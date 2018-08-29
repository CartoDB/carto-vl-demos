<template>
  <div id="app">
    <Map basemap="voyager" geom="points"/>
  </div>
</template>

<script>
import Map from './components/Map.vue'

export default {
  name: 'app',
  components: {
    Map
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
#app {
  position: absolute;
  height: 100%;
  width: 100%;
}
</style>
