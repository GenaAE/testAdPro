<template>
  <div>
    <h1>Привет</h1>
    <button @click="fetchProjects" type="button">Give me projects</button>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  methods: {
    async fetchProjects() {
      try {
        const res = await axios.get(
          'https://dev.aicap.tech/api/v1/interview/projects/'
        );
        console.log(res);
      } catch (err) {
        alert('problems');
      }
    },
  },
};
</script>

<style></style>
