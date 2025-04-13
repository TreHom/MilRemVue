<template>
    <l-marker :lat-lng="props.position">
      <l-popup :options="{ autoClose: false }">
        <div class="waypointPopup" :class="{ 'saved-waypoint': props.isSaved }">
          <button @click="$emit('addWaypoint')">Add Waypoint</button>
          <button @click="$emit('moveVehicle', props.position)">Move Vehicle Here</button>
          <button @click="$emit('discard', props.id)" class="delete">Discard</button>
        </div>
      </l-popup>
    </l-marker>
  </template>
<!-- popups need to be inside l markers to work it seems, or i am getting my fever back, no idea -->

  <script setup>
  import { LMarker, LPopup } from '@vue-leaflet/vue-leaflet'
  import { defineProps } from 'vue'
  
  const props = defineProps({
    position: {
      type: Array,
      required: true
    },
    isSaved: {
      type: Boolean,
      default: false
    },
    id: {
      type: [Number, String],
      default: null
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
  
  .saved-waypoint {
    background-color: #e8f5e9;
    border-radius: 8px;
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
  button.delete {
  background-color: #f44336;
}
  </style>

<!-- Used AI autocomplete to encapsulate LPopup inside LMarker and for styles
 in addition complelty forgot that comments need to be in HTML format to work -->