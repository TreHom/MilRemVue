<template>
  <l-map
    style="height: 1000px; width: 100%;"
    :zoom="13"
    :center="[58.3776, 26.7290]"
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


const tileUrl = 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
const attribution = '&copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors'
</script>
