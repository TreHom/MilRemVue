<template>
  <l-map
    style="height: 1000px; width: 100%;"
    :zoom="100"
    :center="vehiclePosition"
  >
    <l-tile-layer
      :url="tileUrl"
      :attribution="attribution"
    />
  </l-map>
</template>

<script setup>
import 'leaflet/dist/leaflet.css'
import { LMap, LTileLayer} from '@vue-leaflet/vue-leaflet'

const props = defineProps({
  vehiclePosition: {
    type: Array,
    required: true
  }
})

const tileUrl = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
const attribution = '&copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors'

</script>
