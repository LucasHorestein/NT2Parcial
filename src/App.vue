<template>
  <div id="app" class="container-fluid mt-3">
    <div class="jumbotron">
      <h3>Parcial Lucas Horestein </h3>
      <br>
      <Navbar />
      <router-view></router-view>

    </div>
  </div>
</template>

<script>

import Navbar from './componentes/Navbar.vue'
export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>
#app {
}

h3 {
  color: #5f5fe0;
}
</style>
