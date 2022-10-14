<template>
  <div class="px-4 w-50 mx-auto">
    <h1 class="mt-3">{{ msg }}</h1>
    <b-form class="mt-3" @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group id="input-group-3" label="Unidades" label-align="left" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.op1"
          :options="unidades"
          required
        ></b-form-select>
      </b-form-group>

      <!-- Componente de conversión -->
      <div class="d-flex flex-row mt-4">
        <!-- Primeras unidades -->
        <div class="w-50">
          <div class="d-flex flex-column">
            <div>
              <b-form-group
                id="input-group-1"
              >
                <b-form-input
                  @input="checkV1"
                  id="input-1"
                  v-model="form.value1"
                  type="number"
                  placeholder="0"
                  required
                ></b-form-input>
              </b-form-group>
            </div>

            <div>
              <b-form-group id="input-group-3" class="mt-n3">
                <b-form-select
                  @change="checkV1"
                  id="input-3"
                  v-model="form.op2"
                  :options="lista_opciones_1"
                  required
                ></b-form-select>
              </b-form-group>
            </div>
          </div>
        </div>
        <!-- Fin primeras unidades -->

        <div class="px-2" v-bind:style="{'font-size': '26px'}">=</div>

        <!-- Segundas unidades -->
        <div class="w-50">
          <div class="d-flex flex-column">
            <div>
              <b-form-group
                id="input-group-1"
              >
                <b-form-input
                  @input="checkV2"
                  id="input-1"
                  v-model="form.value2"
                  type="number"
                  placeholder="0"
                  required
                ></b-form-input>
              </b-form-group>
            </div>

            <div>
              <b-form-group id="input-group-3" class="mt-n3">
                <b-form-select
                  @change="checkV2"
                  id="input-3"
                  v-model="form.op3"
                  :options="lista_opciones_1"
                  required
                ></b-form-select>
              </b-form-group>
            </div>
          </div>
        </div>
        <!-- Fin segundas unidades -->
      </div>
    </b-form>


    <div>
      <b-button id="show-btn" @click="showModal">Open Modal</b-button>
      <b-button id="toggle-btn" @click="toggleModal">Toggle Modal</b-button>

      <b-modal ref="my-modal" hide-footer title="Using Component Methods">
        <div class="d-block text-center">
          <h3>Hello From My Modal!</h3>
        </div>
        <b-button class="mt-3" variant="outline-danger" block @click="hideModal">Close Me</b-button>
        <b-button class="mt-2" variant="outline-warning" block @click="toggleModal">Toggle Me</b-button>
      </b-modal>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Conversiones',
    props: {
      msg: String,
    },
    mounted() {
      this.$refs['my-modal'].show();
    },
    data() {
      return {
        unidades: [
          { text: 'Potencia eléctrica', value: 1 }
        ],
        // Esta lista cambiará en futuro de acuerdo a las opciones que se vayan ingresando al selector principal de unidades
        lista_opciones_1: [
          { text: 'decibelio-milivatio (dBm)', value: 1 },
          { text: 'Watts (w)', value: 2 }
        ],
        lista_valores: [
          { f1: (value) => 10 * Math.log10(1000 * value) },
          { f2: (value) => Math.pow(10, (value/10)) }
        ],
        form: {
          value1: null,
          value2: null,
          op1: 1,
          op2: 1,
          op3: 1,
        },
        show: true
      }
    },
    methods: {
      getSelectedItem: function(myarg) { // Just a regular js function that takes 1 arg
        console.log(myarg);
      },
      checkV1() {
        if (this.form.op2 == this.form.op3) this.form.value2 = this.form.value1;
        else if (this.form.op2 == 2) {
          let f1 = this.lista_valores[0];
          this.form.value2 = f1.f1(parseFloat(this.form.value1));
        } else {
          let f2 = this.lista_valores[1];
          this.form.value2 = f2.f2(parseFloat(this.form.value1));
        }
      },
      checkV2() {
        if (this.form.op2 == this.form.op3) this.form.value1 = this.form.value2;
        else if (this.form.op3 == 2) {
          let f1 = this.lista_valores[0];
          this.form.value1 = f1.f1(parseFloat(this.form.value2));
        } else {
          let f2 = this.lista_valores[1];
          this.form.value1 = f2.f2(parseFloat(this.form.value2));
        }
      },
      onSubmit(event) {
        event.preventDefault()
        alert(JSON.stringify(this.form))
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.value1 = null,
        this.value2 = null,
        this.op1 = 1,
        this.op2 = 1,
        this.op3 = 1,
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },
      showModal() {
        this.$refs['my-modal'].show();
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
