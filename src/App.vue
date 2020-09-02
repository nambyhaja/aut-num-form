<template>
  <div id="vue-app">
    <AutNumForm msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import AutNumForm from './components/AutNumForm.vue'

export default {
  name: 'App',
  components: {
    AutNumForm
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
