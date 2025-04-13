<template>
  <l-map
    ref="mapRef"
    style="height: 90%; width: 100%;"
    :zoom="100"
    :center="props.vehiclePosition"
    @ready="onMapReady"
  >
    <l-tile-layer :url="tileUrl" :attribution="attribution" />

    
    <VehicleMarker :vehiclePosition="props.vehiclePosition" />

    <Waypoint 
      v-if="showPopup"
      :position="popupLocation"
      @addWaypoint="handleAddWaypoint"
      @moveVehicle="handleMoveVehicle"
      @discard="handleDiscard"
    />
  </l-map>
</template>

<script setup>
import 'leaflet/dist/leaflet.css'
import { LMap, LTileLayer } from '@vue-leaflet/vue-leaflet'
import { defineProps, ref } from 'vue'
import VehicleMarker from './VehicleMarker.vue'
import Waypoint from './WayPoint.vue'

// Vehicle position prop
const props = defineProps({
  vehiclePosition: {
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
  console.log("Add Waypoint clicked at:", popupLocation.value)
}

function handleMoveVehicle() {
  console.log("Move Vehicle clicked at:", popupLocation.value)
}

function handleDiscard() {
  console.log("Discard clicked at:", popupLocation.value)
}
</script>
