<template>
  <button class="engine-start-btn" :class="{ 'engine-running': props.engineStatus }" @click="toggleEngine">
    <img src="../assets/engine-svgrepo-com.svg" alt="Engine Icon" class="engine-icon">
    <span>{{ engineStatus ? 'Engine Running' : 'Engine Start' }}</span>
  </button>
</template>

<script setup>
import { defineProps,defineEmits } from 'vue';

const props = defineProps({
  engineStatus: {
    type: Boolean,
    required: true
  }
});
//defines component named updateEngineStatus to emit
const emit = defineEmits(['updateEngineStatus']);
//emits component named updateEngineStatus with value !props.engineStatus
const toggleEngine = () => {
  emit('updateEngineStatus', !props.engineStatus);
};

</script>

<style scoped>
.engine-start-btn {
  position: absolute;
  top: 20px;
  right: 20px;
  z-index: 1000;
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 16px;
  background-color: rgba(128, 128, 128, 0.8);
  border: 2px solid black;
  color: white;
  border-radius: 4px;
  cursor: pointer;
  font-weight: 500;
}

.engine-start-btn.engine-running {
  background-color: rgba(255, 0, 0, 0.8);
}

.engine-start-btn:hover {
  background-color: rgba(128, 128, 128, 0.9);
}

.engine-start-btn.engine-running:hover {
  background-color: rgba(255, 0, 0, 0.9);
}

.engine-icon {
  width: 50px;
  height: 50px;
  filter: brightness(0) invert(1);
}
</style>