<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/covid-19.png">
    <div class="date">
      {{  new Date() | moment("llll") }}
    </div>
    <Api />
    <a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/uqlpfWJ">
      <img src="https://cdn.buymeacoffee.com/buttons/bmc-new-btn-logo.svg" alt="Buy me a coffee">
    </a>
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
  padding-top: 4rem;
}
</style>
