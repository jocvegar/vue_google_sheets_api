<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Api />
    <Chart />
  </div>
</template>

<script>
import Api from './components/Api.vue'
import Chart from './components/Chart.vue'

export default {
  name: 'App',
  components: {
    Api,
    Chart
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
