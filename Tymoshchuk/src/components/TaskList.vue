<template>
  <ul class="list-group">
    <li v-for="(task, index) in tasks" :key="index" class="list-group-item d-flex justify-content-between align-items-center">
      <span>{{ task.name }}</span>
      <span class="badge bg-primary rounded-pill" v-if="task.status === 'In progress'">{{ task.status }}</span>
      <span class="badge bg-success rounded-pill" v-else>{{ task.status }}</span>
      <div>
        <button @click="finishTask(index)" class="btn btn-sm btn-success me-2">Finish</button>
        <button @click="deleteTask(index)" class="btn btn-sm btn-danger">Delete</button>
      </div>
    </li>
  </ul>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'
const props = defineProps(['tasks'])
const emits = defineEmits(['deleteTask', 'finishTask'])
const deleteTask = (index) => {
  emits('deleteTask', index)
}
const finishTask = (index) => {
  emits('finishTask', index)
}
</script>
