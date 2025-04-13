<template>
  <div class="app-container">
    <EngineStart :engineStatus="engineStatus" @updateEngineStatus="updateEngineStatus" />
    <MapApplication :vehiclePosition="vehiclePosition" />
    <MovementControls :engineStatus="engineStatus" @move="move" />
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

    // Movement step size
    const STEP_SIZE = 0.0001

    const move = (direction) => {
      if (!engineStatus.value) return

      switch (direction) {
        case 'north':
          vehiclePosition.value = [vehiclePosition.value[0] + STEP_SIZE, vehiclePosition.value[1]]
          break
        case 'south':
          vehiclePosition.value = [vehiclePosition.value[0] - STEP_SIZE, vehiclePosition.value[1]]
          break
        case 'east':
          vehiclePosition.value = [vehiclePosition.value[0], vehiclePosition.value[1] + STEP_SIZE]
          break
        case 'west':
          vehiclePosition.value = [vehiclePosition.value[0], vehiclePosition.value[1] - STEP_SIZE]
          break
      }
    }

    return {
      vehiclePosition,
      engineStatus,
      updateEngineStatus,
      move
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