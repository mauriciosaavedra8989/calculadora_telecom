<template>
    <div class="px-4 w-50 mx-auto">
      <h1 class="mt-3">{{ msg }}</h1>
      <b-form-group id="input-group-3" label="Fórmulas" label-align="left" label-for="input-3">
        <b-form-select
          @change="changeValueFunction"
          id="input-3"
          v-model="form.op1"
          :options="formulas"
          required
        ></b-form-select>
      </b-form-group>
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
            { text: 'Teorema de Shannon-Hartley', value: 1 },
            { text: 'Indice de ruido', value: 2 },
            { text: 'Potencia de ruido térmico', value: 3 },
            { text: 'Voltaje de ruido para resistencias internas', value: 4 },
            { text: 'Movimiento Armónico Simple (M.A.S)', value: 5 },
            { text: 'decibelio-milivatio (dBm) → Watts (w)', value: 6 },
          ],
          // Esta lista cambiará en futuro de acuerdo a las opciones que se vayan ingresando al selector principal de fórmulas
          lista_valores: [
            'I = B x log2(1 + s/n) \n\n Donde: \n I = Capacidad de información [bits por segundo] \n B = Ancho de banda [Hz] \n s/n = Relación de potencia de señal a ruido',
            'NF(dB) = 10 * log(F)',
            'N = KTB (w) \n\n Donde: \n B = El ancho de banda (Hz) \n K = 1,38 x 10^-23 J/K. (Cte. de Boltzmann) \n T = Temperatura (absoluta), en Kelvin.',
            'Vn = √(4RKTB) \n\n Donde: \n B = El ancho de banda (Hz) \n K = 1,38 x 10^-23 J/K. (Cte. de Boltzmann) \n T = Temperatura (absoluta), en Kelvin.',
            'X = A Sen(wt+ Φ) \n\n Donde: \n A es la amplitud. \n ω la frecuencia angular. \n ω t+φ la fase. \n φ la fase inicial.',
            '10 * log(1000 * dBm)'
          ],
          form: {
            op1: 1,
          },
          show: true
        }
      },
      methods: {
        changeValueFunction: function(myarg) { // Just a regular js function that takes 1 arg
          this.value = this.lista_valores[myarg - 1]
        },
      },
      created() {
        this.changeValueFunction(1)
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
  