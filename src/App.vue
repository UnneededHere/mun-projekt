<template>
  <test :startTime="10"></test>
</template>

<script>
import test from './components/BigClock.vue'

export default {
  name: 'App',
  components: {
    test
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
