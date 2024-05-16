<template>
  <div>
    <input type="text" v-model="newTask" class="form-control mb-3" placeholder="Enter task">
    <button @click="addTask" class="btn btn-primary">Add Task</button>
  </div>
</template>

<script setup>
import {ref, defineEmits} from 'vue'

const emits = defineEmits(['addTask'])

const newTask = ref('')

const addTask = () => {
  if (newTask.value.trim() !== '') {
    emits('addTask', newTask.value)
    newTask.value = ''
  }
}
</script>

