<template>
  <div id="app" v-bind:style="{'min-height': '100vh'}">
    <nav>
      <router-link to="/">Conversiones</router-link> |
      <router-link to="/formulas">Fórmulas</router-link> |
      <router-link to="/ejercicios">Ejercicios</router-link> |
      <router-link to="/perdidas">Perdidas</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
