<template>
    <div class="home">
      <img alt="Vue logo" src="../assets/logo.png" v-bind:style="{height: '40px', width: '40px'}">
      <Ejercicios msg="Playground - Ejercicios"/>
    </div>
  </template>
  
  <script>
  // @ is an alias to /src
  import Ejercicios from '@/components/Ejercicios.vue'
  
  export default {
    name: 'EjerciciosView',
    components: {
      Ejercicios
    }
  }
  </script>