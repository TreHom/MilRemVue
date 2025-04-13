<template>
  <div class="app-container">
    <WaypointList 
      :waypoints="waypoints"
      @delete="discardWaypoint"
      @rename="renameWaypoint"
      @drive="moveVehicle"
    />
    <EngineStart :engineStatus="engineStatus" @updateEngineStatus="updateEngineStatus" />
    <MapApplication 
      :vehiclePosition="vehiclePosition" 
      :waypoints="waypoints"
      @addWaypoint="addWaypoint"
      @moveVehicle="moveVehicle"
      @discardWaypoint="discardWaypoint"
    />
    <MovementControls :engineStatus="engineStatus" @move="move" />
  </div>
</template>

<script>
import MapApplication from './components/MapApplication.vue'
import EngineStart from './components/EngineStart.vue'
import MovementControls from './components/MovementControls.vue'
import WaypointList from './components/WaypointList.vue'
import { ref } from 'vue'

export default {
  name: 'App',
  components: {
    MapApplication,
    EngineStart,
    MovementControls,
    WaypointList
  },
  setup() {
    const vehiclePosition = ref([58.3776, 26.7290])
    const engineStatus = ref(false)
    const waypoints = ref([])
    
    const updateEngineStatus = (newStatus) => {
      engineStatus.value = newStatus
    }

    const addWaypoint = (waypoint) => {
      waypoints.value.push(waypoint)
      console.log('Waypoints:', waypoints.value)
    }

    const discardWaypoint = (id) => {
      waypoints.value = waypoints.value.filter(wp => wp.id !== id)
      console.log('Waypoint discarded:', id)
      console.log('Remaining waypoints:', waypoints.value)
    }

    const renameWaypoint = ({ id, newName }) => {
      const waypoint = waypoints.value.find(wp => wp.id === id)
      if (waypoint) {
        waypoint.name = newName
        console.log('Waypoint renamed:', waypoint)
      }
    }

    const moveVehicle = (position) => {
      // If position is a waypoint object, use its location
      const newPosition = Array.isArray(position) ? position : position.location
      vehiclePosition.value = newPosition
      console.log('Vehicle moved to:', newPosition)
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
      waypoints,
      updateEngineStatus,
      addWaypoint,
      discardWaypoint,
      renameWaypoint,
      moveVehicle,
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