<script setup>
import { reactive, ref, computed } from 'vue'

// Define exactly what this component yields to the parent
const emit = defineEmits(['submit-entry'])

const taskTypes = ['Teaching', 'Research', 'Administrative', 'Meeting', 'Other']

const form = reactive({
  date: new Date().toISOString().split('T')[0],
  startTime: '',
  endTime: '',
  task: '',
  description: ''
})

const errorMsg = ref('')

// Computed property to disable button if incomplete
const isFormValid = computed(() => {
  return form.date && form.startTime && form.endTime && form.task && form.description
})

const submitForm = () => {
  errorMsg.value = ''
  
  if (!isFormValid.value) {
    errorMsg.value = 'All fields are required.'
    return
  }

  // Core Validation: Time boundaries
  if (form.endTime <= form.startTime) {
    errorMsg.value = 'End time must be cleanly after start time.'
    return
  }

  // Fire event to View component with the pure data payload
  emit('submit-entry', { ...form })
  
  // Clean up the local UI state
  form.startTime = ''
  form.endTime = ''
  form.task = ''
  form.description = ''
}
</script>

<template>
  <div class="form-container">
    <form @submit.prevent="submitForm">
      
      <div class="form-group">
        <label>Date</label>
        <input type="date" v-model="form.date" required />
      </div>

      <div class="form-row">
        <div class="form-group half">
          <label>Start Time</label>
          <input type="time" v-model="form.startTime" required />
        </div>
        <div class="form-group half">
          <label>End Time</label>
          <input type="time" v-model="form.endTime" required />
        </div>
      </div>

      <div class="form-group">
        <label>Task Type</label>
        <select v-model="form.task" required>
          <option disabled value="">Please select one</option>
          <option v-for="task in taskTypes" :key="task" :value="task">{{ task }}</option>
        </select>
      </div>

      <div class="form-group">
        <label>Description</label>
        <textarea v-model="form.description" rows="3" required placeholder="Describe your activity briefly"></textarea>
      </div>

      <div v-if="errorMsg" class="error-msg">{{ errorMsg }}</div>

      <button type="submit" class="submit-btn" :disabled="!isFormValid">Log Time</button>
    </form>
  </div>
</template>

<style scoped>
.form-container {
  background: white;
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  max-width: 500px;
}

.form-group {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
}

.form-row {
  display: flex;
  gap: 15px;
}

.half {
  flex: 1;
}

label {
  font-weight: 500;
  margin-bottom: 8px;
  color: var(--primary-color);
}

input, select, textarea {
  padding: 10px;
  border: 1px solid var(--border-color);
  border-radius: 4px;
  font-size: 1rem;
}

input:focus, select:focus, textarea:focus {
  outline: none;
  border-color: var(--accent-color);
}

.error-msg {
  color: #dc3545;
  margin-bottom: 15px;
  font-size: 0.9rem;
}

.submit-btn {
  background-color: var(--accent-color);
  color: white;
  border: none;
  padding: 12px 20px;
  border-radius: 4px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  width: 100%;
  transition: background-color 0.2s;
}

.submit-btn:hover {
  background-color: #38a169;
}

.submit-btn:disabled {
  background-color: #a0aec0;
  cursor: not-allowed;
}
</style>
