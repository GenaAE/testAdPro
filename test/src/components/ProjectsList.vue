<template lang="">
  <div>
    <div class="pro" v-for="project in projects" :key="project.id">
      <div>id: {{ project.id }}</div>
      <div>Status: {{ project.status }}</div>
      <div>Title: {{ project.title }}</div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    projects: {
      type: Array,
      required: true,
    },
  },
};
</script>
<style scoped>
.pro {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  border: 2px solid #5baf6f;
  margin-top: 10px;
}
</style>
