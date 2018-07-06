<template>
  <div id="app">
    <index/>
  </div>
</template>

<script>
import Index from './components/index'

export default {
  name: 'App',
  components: {
    Index
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  
}
html body{
  position: relative;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: 0;
  padding: 0;
}
ul,li{ padding:0;margin:0;list-style:none}
</style>
