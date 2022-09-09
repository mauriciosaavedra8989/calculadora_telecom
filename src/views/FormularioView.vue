<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" v-bind:style="{height: '40px', width: '40px'}">
    <Formulas msg="Libro de fórmulas"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Formulas from '@/components/Formulas.vue'

export default {
  name: 'FormularioView',
  components: {
    Formulas
  }
}
</script>