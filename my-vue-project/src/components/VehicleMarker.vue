<template>
    <l-marker :lat-lng="position" :icon="vehicleIcon" />
</template>

<script setup>
import { LMarker } from '@vue-leaflet/vue-leaflet'

const props = defineProps({
    position: {
        type: Array,
        required: true 
    }
})
</script>