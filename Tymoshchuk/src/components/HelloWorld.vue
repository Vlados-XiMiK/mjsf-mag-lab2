<template>
  <section class="vh-100" style="background-color: #eee;">
    <div class="container py-5 h-100">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col col-lg-9 col-xl-7">
          <div class="card rounded-3">
            <div class="card-body p-4">

              <h4 class="text-center my-3 pb-3">To Do App</h4>

              <form class="row row-cols-lg-auto g-3 justify-content-center align-items-center mb-4 pb-2" @submit.prevent="addTask">
                <div class="col-12">
                  <div class="form-outline">
                    <input type="text" v-model="newTask" class="form-control" />
                    <label class="form-label" for="form1">Enter a task here</label>
                  </div>
                </div>

                <div class="col-12">
                  <button type="submit" class="btn btn-primary">Save</button>
                </div>

                <div class="col-12">
                  <button type="button" class="btn btn-warning" @click="getTasks">Get tasks</button>
                </div>
              </form>

              <table class="table mb-4" v-if="tasks.length > 0">
                <thead>
                <tr>
                  <th scope="col">No.</th>
                  <th scope="col">Todo item</th>
                  <th scope="col">Status</th>
                  <th scope="col">Actions</th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="(task, index) in tasks" :key="index">
                  <th scope="row">{{ index + 1 }}</th>
                  <td>{{ task.name }}</td>
                  <td>{{ task.status }}</td>
                  <td>
                    <button type="button" class="btn btn-danger" @click="deleteTask(index)">Delete</button>
                    <button type="button" class="btn btn-success ms-1" @click="finishTask(index)" v-if="task.status === 'In progress'">Finish</button>
                  </td>
                </tr>
                </tbody>
              </table>

            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const tasks = ref([])
const newTask = ref('')

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push({ name: newTask.value, status: 'In progress' })
    newTask.value = ''
  }
}

const deleteTask = index => {
  tasks.value.splice(index, 1)
}

const finishTask = index => {
  tasks.value[index].status = 'Finished'
}

const getTasks = () => {
  // Можна додати запрос на виведення з бд
  tasks.value = [
    { name: 'Buy groceries for next week', status: 'In progress' },
    { name: 'Renew car insurance', status: 'In progress' },
    { name: 'Sign up for online course', status: 'In progress' }
  ]
}
</script>

<style scoped>
@import url('https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css');
@import url('https://cdn.jsdelivr.net/npm/bootstrap-icons@1.5.0/font/bootstrap-icons.css');

</style>