<script>
export default {
  setup() {
    const name = 'Lora Mitova'
    const status = 'pending'
    const tasks = ['Task One', 'Task Two', 'Task Tree']

  }
}
</script>

<template>
  <h1>Hello</h1>
  <h2>{{ name }}</h2>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else="status">User is inactive</p>

  <h3>Tasks: </h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

  <br />
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click="toggleStatus">Change Status</button>


</template>

<style scoped></style>