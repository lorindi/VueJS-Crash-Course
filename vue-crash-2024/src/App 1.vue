<!-- options -->
<script>
export default {
  data() {
    return {
      name: 'Lora Mitova',
      status: 'pending',
      tasks: ['Task One', 'Task Two', 'Task Tree'],
      link: 'https://www.google.com/'
    }
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'pending'
      } else if (this.status === 'pending') {
        this.status = 'inactive'
      } else {
        this.status = 'active'
      }
    }
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

  <!-- <a v-bind:href="link">Click for Google</a> -->
  <a :href="link">Click for Google</a>
  <br />
  <!-- <button v-on:click="toggleStatus">Change Status</button> -->
  <button @click="toggleStatus">Change Status</button>


</template>

<style scoped>
h1 {
  color: aqua;
}
</style>