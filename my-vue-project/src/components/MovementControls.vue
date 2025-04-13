<template>
    <div class="control-panel">
      <button @click="handleMove('north')" :class="{ 'inactive': !props.engineStatus }">↑</button>
      <div class="horizontal-controls">
        <button @click="handleMove('west')" :class="{ 'inactive': !props.engineStatus }">←</button>
        <button @click="handleMove('east')" :class="{ 'inactive': !props.engineStatus }">→</button>
      </div>
      <button @click="handleMove('south')" :class="{ 'inactive': !props.engineStatus }">↓</button>
    </div>

    <!-- Simple popup -->
    <div v-if="showPopup" class="engine-popup">
      <div class="popup-content">
        <p>Please turn the engine on first!</p>
        <button @click="showPopup = false">OK</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits, ref } from 'vue';
  
  const props = defineProps({
    engineStatus: {
      type: Boolean,
      required: true
    }
  })

  const emit = defineEmits(['move'])
  const showPopup = ref(false)

  function handleMove(direction) {
    if (props.engineStatus) {
      emit('move', direction)
    } else {
      showPopup.value = true
    }
  }
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
  
  button.inactive {
    background: #eee;
  }
  
  button:hover {
    background: #f0f0f0;
  }

  /* Popup styles */
  .engine-popup {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1001;
  }

  .popup-content {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    text-align: center;
  }

  .popup-content p {
    margin: 0 0 15px 0;
  }

  .popup-content button {
    width: auto;
    height: auto;
    padding: 8px 16px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  .popup-content button:hover {
    background-color: #45a049;
  }
  </style>