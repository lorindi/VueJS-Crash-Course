<!-- composition -->
<script setup>
import { ref, onMounted } from 'vue'

const name = ref('Lora Mitova');
const status = ref('pending');
const tasks = ref(['Task One', 'Task Two', 'Task Tree']);
const newTask = ref('')

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending'
  } else if (status.value === 'pending') {
    status.value = 'inactive'
  } else {
    status.value = 'active'
  }
};
const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value)
    newTask.value = ''
  }
}
const deleteTask = (index) => {
  tasks.value.splice(index, 1)
}

onMounted(async () => {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/todos')
    const data = await res.json()
    tasks.value = data.map((task) => task.title)
  }
  catch (err) {
    console.log(err);

  }
})
</script>

<template>
  <h1>Hello</h1>
  <h2>{{ name }}</h2>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else="status">User is inactive</p>

  <form @submit.prevent="addTask"
    style="display: flex; flex-direction: column; align-items:stretch; gap: 10px; margin: 30px 0px;">
    <label for="newTask" style="font-size: 30px; color: aliceblue;">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask">
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks: </h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span style="margin-right: 10px;">
        {{ task }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>

  <br />
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click="toggleStatus">Change Status</button>


</template>

<style></style>