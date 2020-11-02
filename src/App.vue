<template>
  <div id="app">
    <range-slider :max="20" :step="0.5"/>
  </div>
</template>

<script>
import RangeSlider from './components/RangeSlider.vue'

export default {
  name: 'App',
  components: {
    RangeSlider
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
