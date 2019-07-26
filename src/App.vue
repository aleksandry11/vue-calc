<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Calc title="Vue.js Calc With History"/>
  </div>
</template>

<script>
import Calc from './components/Calc.vue';

export default {
  name: 'app',
  components: {
    Calc
  }
}
</script>

<style>
  *, *:after, *:before {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body {
    background-color: #181c2b;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
  img {
    position: relative;
    top: -20px;
  }
</style>
