<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
html,body { margin:0; padding:0; height:100%; width:100%; }
#app {
  font-family: 'Libre Baskerville', 'Nanum Myeongjo', serif, 'Avenir', Helvetica, Arial, sans-serif;
  color: #c9cace;
  text-shadow: 2px 2px 3px rgba(0, 0, 0, 0.8);
  font-size: 1.2em;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
