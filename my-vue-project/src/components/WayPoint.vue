<template>
    <l-marker :lat-lng="props.position">
        //popups need to be inside l markers to work it seems, or i am getting my fever back no idea
      <l-popup :options="{ autoClose: false }">
        <div class="waypointPopup">
          <button @click="$emit('addWaypoint')">Add Waypoint</button>
          <button @click="$emit('moveVehicle')">Move Vehicle Here</button>
          <button @click="$emit('discard')">Discard</button>
        </div>
      </l-popup>
    </l-marker>
  </template>
  
  <script setup>
  import { LMarker, LPopup } from '@vue-leaflet/vue-leaflet'
  import { defineProps } from 'vue'
  
  const props = defineProps({
    position: {
      type: Array,
      required: true
    }
  })
  </script>
  
  <style scoped>
  .waypointPopup {
    display: flex;
    flex-direction: column;
    gap: 8px;
    padding: 8px;
  }
  
  button {
    padding: 8px 16px;
    border: 2px solid black;
    background-color: #4CAF50;
    color: white;
    cursor: pointer;
    font-size: 14px;
  }
  
  button:hover {
    background-color: #45a049;
  }
  </style>
//Used AI autocomplete to encapsulate LPopup inside LMarker and for styles 