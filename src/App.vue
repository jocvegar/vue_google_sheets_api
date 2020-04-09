<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/covid-19.png">
    <div class="date">
      {{  new Date() | moment("llll") }}
    </div>
    <Api />
  </div>
</template>

<script>
import Api from './components/Api.vue'

export default {
  name: 'App',
  components: {
    Api,
  },
}
</script>

<style lang="scss">
html {
  background: rgba(224, 224, 224, 0.2);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.date {
  padding: 3rem 0;
}
</style>
