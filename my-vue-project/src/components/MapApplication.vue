<template>
  <l-map
    ref="mapRef"
    style="height: 90%; width: 80%; left:20%"
    :zoom="100"
    :center="props.vehiclePosition"
    @ready="onMapReady"
  >
    <l-tile-layer :url="tileUrl" :attribution="attribution" />

    <VehicleMarker :vehiclePosition="props.vehiclePosition" />

    <Waypoint 
      v-for="waypoint in props.waypoints"
      :key="waypoint.id"
      :position="waypoint.location"
      :is-saved="true"
      :id="waypoint.id"
      @addWaypoint="handleAddWaypoint"
      @moveVehicle="handleMoveVehicle"
      @discard="handleDiscard"
    />

    <Waypoint 
      v-if="showPopup"
      :position="popupLocation"
      :is-saved="false"
      :id="'temp-' + Date.now()"
      @addWaypoint="handleAddWaypoint"
      @moveVehicle="handleMoveVehicle"
      @discard="handleDiscard"
    />
  </l-map>
</template>

<script setup>
import 'leaflet/dist/leaflet.css'
import { LMap, LTileLayer } from '@vue-leaflet/vue-leaflet'
import { defineProps, ref, defineEmits } from 'vue'
import VehicleMarker from './VehicleMarker.vue'
import Waypoint from './WayPoint.vue'

// Vehicle position and waypoints props
const props = defineProps({
  vehiclePosition: {
    type: Array,
    required: true
  },
  waypoints: {
    type: Array,
    required: true
  }
})

const tileUrl = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
const attribution = '&copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors'


const mapRef = ref(null)
const showPopup = ref(false)
const popupLocation = ref([0, 0])

let pressTimer = null
let map = null
let wasLongPress = false 

const emit = defineEmits(['addWaypoint', 'moveVehicle', 'discardWaypoint'])

function onMapReady(leafletMap) {
  map = leafletMap

  map.on('mousedown', (e) => {
    pressTimer = setTimeout(() => {
      wasLongPress = true
      popupLocation.value = [e.latlng.lat, e.latlng.lng]
      showPopup.value = true
      console.log("Long press triggered at:", popupLocation.value)
    }, 800)
  })

  map.on('mouseup', () => {
    clearTimeout(pressTimer)
    
    setTimeout(() => {
      wasLongPress = false
    }, 10)
  })

  map.on('mousemove', () => {
    clearTimeout(pressTimer)
  })

  map.on('click', () => {
    if (wasLongPress) {
      console.log("Click suppressed after long press")
      return
    }

    if (showPopup.value) {
      showPopup.value = false
      console.log("Map clicked — hiding popup")
    }
  })
}


function handleAddWaypoint() {
  const waypoint = {
    id: Date.now(), // Use timestamp as unique ID
    name: `Waypoint ${Date.now()}`,
    location: popupLocation.value
  }
  emit('addWaypoint', waypoint)
  console.log("Add Waypoint clicked at:", waypoint)
}

function handleMoveVehicle(position) {
  emit('moveVehicle', position)
  showPopup.value = false
  console.log("Move Vehicle clicked at:", position)
}

function handleDiscard(id) {
  emit('discardWaypoint', id)
  showPopup.value = false
  console.log("Discard clicked for waypoint:", id)
}
</script>
