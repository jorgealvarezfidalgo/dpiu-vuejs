<template>
  <div id="app">
    <h1 class="mb-4">Práctica 5 DPIU - Listado de Naves</h1>
    <Listado/>
	
  </div>
</template>

<script>
import Listado from './components/Listado.vue'

import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

export default {
  name: 'App',
  components: {
    Listado
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
