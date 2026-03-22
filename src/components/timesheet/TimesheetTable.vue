<script setup>
defineProps({
  data: {
    type: Array,
    required: true,
    default: () => []
  }
})
</script>

<template>
  <div class="table-container">
    <table class="data-table">
      <thead>
        <tr>
          <th>Date</th>
          <th>Task</th>
          <th>Time Range</th>
          <th>Description</th>
        </tr>
      </thead>
      <tbody>
        <tr v-if="data.length === 0">
          <td colspan="4" class="empty-state">No timesheet entries found.</td>
        </tr>
        <tr v-for="entry in data" :key="entry.id" class="data-row">
          <td>{{ entry.date }}</td>
          <td><span class="badge">{{ entry.task }}</span></td>
          <td>{{ entry.startTime }} - {{ entry.endTime }}</td>
          <td>{{ entry.description }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.table-container {
  background: white;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.05);
  overflow: hidden;
  margin-top: 20px;
}

.data-table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 15px 20px;
  text-align: left;
  border-bottom: 1px solid var(--border-color);
}

th {
  background-color: #f8fafc;
  color: #64748b;
  font-weight: 600;
  text-transform: uppercase;
  font-size: 0.85rem;
  letter-spacing: 0.05em;
}

.data-row:hover {
  background-color: #f8fafc;
  transition: background-color 0.2s ease;
}

.empty-state {
  text-align: center;
  padding: 30px;
  color: #94a3b8;
  font-style: italic;
}

.badge {
  background-color: #e2e8f0;
  color: #475569;
  padding: 4px 10px;
  border-radius: 12px;
  font-size: 0.85rem;
  font-weight: 500;
}
</style>
