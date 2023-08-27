<template lang="">
  <div>
    <transition-group name="pro-list">
      <div class="pro" v-for="project in projects" :key="project.id">
        <div>id: {{ project.id }}</div>
        <div>Status: {{ project.status }}</div>
        <div>Title: {{ project.title }}</div>
      </div>
    </transition-group>
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

.pro-list-item {
  display: inline-block;
  margin-right: 10px;
}
.pro-list-enter-active,
.pro-list-leave-active {
  transition: all 1s;
}
.pro-list-enter, .pro-list-leave-to /* .list-leave-active до версии 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
.pro-list-move {
  transition: transform 1s;
}
</style>
