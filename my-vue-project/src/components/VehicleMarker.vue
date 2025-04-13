<template>
    <l-marker :lat-lng="props.vehiclePosition" />
</template>

<script setup>
import { LMarker } from '@vue-leaflet/vue-leaflet'
import { defineProps } from 'vue'

const props = defineProps({
    vehiclePosition: {
        type: Array,
        required: true 
    }
})
</script>