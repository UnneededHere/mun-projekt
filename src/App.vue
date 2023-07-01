<template>
  <initial-menu></initial-menu>
</template>

<script>
import InitialMenu from './components/InitialMenu.vue'

export default {
  name: 'App',
  components: {
    InitialMenu
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
