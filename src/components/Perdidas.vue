<template>
  
      
    <!-- Tabla - primera sección -->
    <p class="text-left">Number of mated connectors</p>
    <div class="d-flex justify-content-between align-items-start">
      <input type="number" name="" id="" placeholder="0">
      <p>X</p>
      <p>0.75 dB = </p>
      <input type="number" name="" id="" placeholder="0">
      <p>dB</p>
    </div>

    <!-- Tabla - segunda sección -->
    <p class="text-left">Number of splices?</p>
    <div class="d-flex justify-content-between align-items-start">
      <input type="number" name="" id="" placeholder="0">
      <p>X</p>
      <p>0.3 dB = </p>
      <input type="number" name="" id="" placeholder="0">
      <p>dB</p>
    </div>

    <!-- Tabla - tercera sección -->
    <p class="text-left">Length of fiber in meters?</p>
    <div class="d-flex justify-content-between align-items-start">
      <input type="number" name="" id="" placeholder="0">
      <p>X</p>
      <p>0.0035 dB = </p>
      <input type="number" name="" id="" placeholder="0">
      <p>dB</p>
    </div>

    
  </template>
  
  <script>
    export default {
      name: 'Perdidas',
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

        showModal() {
        this.$refs['my-modal'].show()
      },
      hideModal() {
        this.$refs['my-modal'].hide()
      },
      toggleModal() {
        // We pass the ID of the button that we want to return focus to
        // when the modal has hidden
        this.$refs['my-modal'].toggle('#toggle-btn')
      }, 


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
      mounted: function () {
  this.$nextTick(function () {
    this.$refs['my-modal'].show()
    
  })
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
  