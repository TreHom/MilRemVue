<template>
  <div class="app-container">
    <EngineStart :engineStatus="engineStatus" @updateEngineStatus="updateEngineStatus" />
    <MapApplication :vehiclePosition="vehiclePosition" />
    <MovementControls :engineStatus="engineStatus" />
  </div>
</template>

<script>
import MapApplication from './components/MapApplication.vue'
import EngineStart from './components/EngineStart.vue'
import MovementControls from './components/MovementControls.vue'
import { ref } from 'vue'

export default {
  name: 'App',
  components: {
    MapApplication,
    EngineStart,
    MovementControls
  },
  setup() {
    const vehiclePosition = ref([58.3776, 26.7290])
    const engineStatus = ref(false)
    const updateEngineStatus = (newStatus) => {
      engineStatus.value = newStatus
    }

    return {
      vehiclePosition,
      engineStatus,
      updateEngineStatus
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
}

.app-container {
  position: relative;
  width: 100%;
  height: 100vh;
  margin: 0;
  padding: 0;
}
</style>
