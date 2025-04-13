<template>
  <div class="waypoint-list">
    <h2>Saved Waypoints</h2>
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Location</th>
        </tr>
      </thead>
      <tbody>
        <tr 
          v-for="waypoint in props.waypoints" 
          :key="waypoint.id"
          @click="showWaypointOptions(waypoint)"
          class="waypoint-row"
        >
          <td>{{ waypoint.name }}</td>
          <td>{{ formatLocation(waypoint.location) }}</td>
        </tr>
      </tbody>
    </table>

    <!-- Waypoint Options Popup -->
    <div v-if="selectedWaypoint" class="waypoint-options-popup">
      <div class="popup-content">
        <h3>{{ selectedWaypoint.name }}</h3>
        <div class="options">
          <button @click="handleRename">Rename</button>
          <button @click="handleDrive">Drive Here</button>
          <button @click="handleDelete" class="delete">Delete</button>
        </div>
        <button @click="closePopup" class="close">Close</button>
      </div>
    </div>

    <!-- Rename Input Popup -->
    <div v-if="showRenameInput" class="rename-popup">
      <div class="popup-content">
        <h3>Rename Waypoint</h3>
        <input 
          v-model="newName" 
          @keyup.enter="saveNewName"
          placeholder="Enter new name"
          ref="nameInput"
        />
        <div class="buttons">
          <button @click="saveNewName">Save</button>
          <button @click="cancelRename">Cancel</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'


const props = defineProps({
  waypoints: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['delete', 'rename', 'drive'])

const selectedWaypoint = ref(null)
const showRenameInput = ref(false)
const newName = ref('')
const nameInput = ref(null)

function formatLocation(location) {
  return `[${location[0].toFixed(4)}, ${location[1].toFixed(4)}]`
}

function showWaypointOptions(waypoint) {
  selectedWaypoint.value = waypoint
}

function closePopup() {
  selectedWaypoint.value = null
}

function handleRename() {
  newName.value = selectedWaypoint.value.name
  showRenameInput.value = true
  // Focus the input after the DOM updates
  setTimeout(() => {
    nameInput.value?.focus()
  }, 0)
}

function saveNewName() {
  if (newName.value.trim()) {
    emit('rename', { id: selectedWaypoint.value.id, newName: newName.value })
    showRenameInput.value = false
    closePopup()
  }
}

function cancelRename() {
  showRenameInput.value = false
  newName.value = ''
}

function handleDrive() {
  emit('drive', selectedWaypoint.value.location)
  closePopup()
}

function handleDelete() {
  emit('delete', selectedWaypoint.value.id)
  closePopup()
}
</script>

<style scoped>
.waypoint-list {
  position: absolute;
  left: 0;
  top: 0;
  width: 300px;
  height: 100%;
  background-color: white;
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
  padding: 20px;
  overflow-y: auto;
}

h2 {
  margin-top: 0;
  color: #2c3e50;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 8px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

.waypoint-row {
  cursor: pointer;
  transition: background-color 0.2s;
}

.waypoint-row:hover {
  background-color: #f5f5f5;
}

.waypoint-options-popup,
.rename-popup {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.popup-content {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  min-width: 300px;
}

.options {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin: 20px 0;
}

button {
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  background-color: #4CAF50;
  color: white;
}

button:hover {
  opacity: 0.9;
}

button.delete {
  background-color: #f44336;
}

button.close {
  background-color: #666;
  width: 100%;
}

input {
  width: 100%;
  padding: 8px;
  margin: 10px 0;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.buttons {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}
</style> 