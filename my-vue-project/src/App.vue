<template>
  <MapApplication :vehiclePosition="vehiclePosition" />
</template>

<script>
import MapApplication from './components/MapApplication.vue'

import { ref } from 'vue'

export default {
  name: 'App',
  components: {
    MapApplication,
    
  },

setup() {
  const vehiclePosition = ref([58.3776, 26.7290])
  return {
    vehiclePosition
  }
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
