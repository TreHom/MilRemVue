<template>
  <l-map
    style="height: 90%; width: 100%;"
    :zoom="100"
    :center="props.vehiclePosition"
  >
    <l-tile-layer
      :url="tileUrl"
      :attribution="attribution"
    />
    <VehicleMarker :vehiclePosition="props.vehiclePosition" />
  </l-map>
</template>

<script setup>
import 'leaflet/dist/leaflet.css'
import { LMap, LTileLayer} from '@vue-leaflet/vue-leaflet'
import { defineProps } from 'vue'
import VehicleMarker from './VehicleMarker.vue'

const props = defineProps({
  vehiclePosition: {
    type: Array,
    required: true
  }
})

const tileUrl = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
const attribution = '&copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors'

</script>
