<template>
    <div class="control-panel">
      <button @click="$emit('move', 'north')" :disabled="!props.engineStatus">↑</button>
      <div class="horizontal-controls">
        <button @click="$emit('move', 'west')" :disabled="!props.engineStatus">←</button>
        <button @click="$emit('move', 'east')" :disabled="!props.engineStatus">→</button>
      </div>
      <button @click="$emit('move', 'south')" :disabled="!props.engineStatus">↓</button>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    engineStatus: {
      type: Boolean,
      required: true
    }
  })
  </script>
  //Had AI write me the initial design for the buttons 
  <style scoped>
  .control-panel {
    position: absolute;
    bottom: 20px;
    left: 50%;
    background: white;
    padding: 10px;
    border-radius: 8px;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
    z-index: 1000;
  }
  
  .horizontal-controls {
    display: flex;
    justify-content: space-between;
    margin: 5px 0;
  }
  
  button {
    width: 50px;
    height: 50px;
    margin: 2px;
    border: 1px solid #ccc;
    border-radius: 4px;
    background: white;
    cursor: pointer;
    font-size: 20px;
  }
  
  button:disabled {
    background: #eee;
    cursor: not-allowed;
  }
  
  button:hover:not(:disabled) {
    background: #f0f0f0;
  }
  </style>