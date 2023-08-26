<template>
  <form @submit.prevent>
    <h4>Поиск</h4>
    <input-pro v-model="projects.title" type="text" placeholder="Название" />
  </form>
</template>

<script>
import InputPro from '../assets/InputPro.vue';
export default {
  components: {
    InputPro,
  },
  data() {
    return {
      projects: {
        title: '',
      },
    };
  },
  methods: {},
  //   watch: {
  //     projects: {
  //       handler(newVal) {
  //         console.log(newVal);
  //       },
  //       deep: true,
  //     },
  //   },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
</style>
