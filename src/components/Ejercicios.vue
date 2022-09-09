<template>
  <div class="px-4 w-50 mx-auto">
    <h1 class="mt-3">{{ msg }}</h1>
    <b-form-group id="input-group-3" label="Ejercicio" label-align="left" label-for="input-3">
      <b-form-select
        @change="changeValueFunction"
        id="input-3"
        v-model="form.op1"
        :options="formulas"
        required
      ></b-form-select>
    </b-form-group>

    <!-- Potencia de ruido térmico -->
    <div v-if="form.op1 == 1" class="mt-3">
        <div class="d-flex flex-row justify-content-between">
          <b-form-group
            id="input-group-1"
          >
            <b-form-input
              label="T"
              label-align="left"
              id="input-1"
              v-model="form.t"
              type="number"
              placeholder="T °C"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group
            id="input-group-2"
          >
            <b-form-input
              label="B"
              label-align="left"
              id="input-1"
              v-model="form.b"
              type="number"
              placeholder="B"
              required
            ></b-form-input>
          </b-form-group>
        </div>
      </div>
      <!-- Fin potencia de ruido térmico-->

      <!-- Voltaje de ruido para resistencias -->
      <div v-if="form.op1 == 2" class="mt-3">
        <div class="d-flex flex-row justify-content-between">
          <b-form-group
            id="input-group-1"
          >
            <b-form-input
              label="R"
              label-align="left"
              id="input-1"
              v-model="form.r"
              type="number"
              placeholder="R (Ω)"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group
            id="input-group-1"
          >
            <b-form-input
              label="T"
              label-align="left"
              id="input-1"
              v-model="form.t"
              type="number"
              placeholder="T °C"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group
            id="input-group-2"
          >
            <b-form-input
              label="B"
              label-align="left"
              id="input-1"
              v-model="form.b"
              type="number"
              placeholder="B"
              required
            ></b-form-input>
          </b-form-group>
        </div>
      </div>
      <!-- Fin voltaje de ruido para resistencias -->

      <!-- Ancho de banda -->
      <div v-if="form.op1 == 3" class="mt-3">
        <div class="d-flex flex-row justify-content-between">
          <b-form-group
            id="input-group-1"
          >
            <b-form-input
              label="W"
              label-align="left"
              id="input-1"
              v-model="form.w"
              type="number"
              placeholder="Potencia w"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group
            id="input-group-2"
          >
            <b-form-input
              label="T"
              label-align="left"
              id="input-1"
              v-model="form.t"
              type="number"
              placeholder="T °C"
              required
            ></b-form-input>
          </b-form-group>
        </div>
      </div>
      <!-- Fin ancho de banda -->

      <!-- longitud de onda -->
      <div v-if="form.op1 == 4" class="mt-3">
        <div class="d-flex flex-row justify-content-between">
          <b-form-group
            id="input-group-1"
          >
            <b-form-input
              label="Frecuencia (kHz)"
              label-align="left"
              id="input-1"
              v-model="form.f1"
              type="number"
              placeholder="Frecuencia (kHz)"
              required
            ></b-form-input>
          </b-form-group>
        </div>
      </div>
      <!-- Fin longitud de onda -->

      <div class="d-flex flex-row justify-content-end">
        <b-button @click="calcResult" variant="outline-primary">Calcular</b-button>
      </div>
    <b-card class="mt-3" header="Detalle">
      <pre class="m-0">{{ value }}</pre>
    </b-card>
  </div>
</template>

<script>
  export default {
    name: 'Formulas',
    props: {
      msg: String,
    },
    data() {
      return {
        value: '',
        formulas: [
          { text: 'Calcular potencia de ruido térmico', value: 1 },
          { text: 'Calcular voltaje de ruido para resistencias internas', value: 2 },
          { text: 'Calcular ancho de banda', value: 3 },
          { text: 'Calcular longitud de onda', value: 4 },
        ],
        form: {
          op1: 1,
          t: null,
          b: null,
          k: null,
          r: null,
          w: null,
          f1: null,
        },
        show: true
      }
    },
    methods: {
      changeValueFunction(item) {
        this.form.op1 = item;
        this.form.t = null;
        this.form.b = null;
        this.form.k = null;
        this.form.r = null;
        this.form.w = null;
        this.form.f1 = null;
        this.value = "";
      },
      calcResult() {
        let k = 1.38 * Math.pow(10, -23);
        switch (this.form.op1) {
          case 1:
            var t = Number(this.form.t) + 273.15;
            var b = Number(this.form.b);

            var result = k * t * b;
            var log = 10 * Math.log10(result / 0.001);
            this.value = `N = ${result} w \n N = ${log} dBm`;
            break;

          case 2:
            var r = Number(this.form.r);
            var t = Number(this.form.t) + 273.15;
            var b = Number(this.form.b);

            var result = Math.sqrt(4 * r * k * t * b);
            this.value = `Vn = ${result}`;
            break;

          case 3:
            var t = Number(this.form.t) + 273.15;
            var w = Number(this.form.w);

            var result = w / (k * t);
            this.value = `B = ${result} Hz`;
            break;

          case 4:
            var khz = Number(this.form.f1);
            var speed_of_light = 3 * Math.pow(10, 8);

            var result = speed_of_light / (khz * 1000);
            this.value = `λ = ${result} m`
            break;
        }
      },
    },
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
