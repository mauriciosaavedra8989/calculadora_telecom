<template>
    <div class="home">
      <img alt="Vue logo" src="../assets/logo.png" v-bind:style="{height: '40px', width: '40px'}">
      <Perdidas msg="Playground - Calculo de perdidas"/>
    </div>


   
    
    
  </template>
  
  <script>
  // @ is an alias to /src
  import Perdidas from '@/components/Perdidas.vue'
  
  export default {
    name: 'perdidaView',
    components: {
      Perdidas
    }
  } 
  </script>