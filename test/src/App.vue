<template>
  <div>
    <h1>Привет</h1>
    <div>
      <button type="button" class="btn">OPPA</button>
      <select-pro v-model="selectedPro" :options="sortOptions" />
      <project-form @create="createPost" />
    </div>
    <button @click="fetchProjects" type="button">Give me projects</button>
    <projects-list :projects="projects" v-if="!isProjectsLoading" />
    <div v-else>
      <semipolar-spinner
        :animation-duration="2000"
        :size="65"
        color="#ff1d5e"
      />

      Loading ...
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import ProjectsList from './components/ProjectsList.vue';
import SemipolarSpinner from './assets/SpinerLoading.vue';
import SelectPro from './assets/SelectPro.vue';
import ProjectForm from './components/ProjectForm.vue';
export default {
  components: {
    ProjectsList,
    SemipolarSpinner,
    SelectPro,
    ProjectForm,
  },
  data() {
    return {
      projects: [],
      isProjectsLoading: false,
      selectedPro: '',
      sortOptions: [
        { value: 'status', name: 'По статусу' },
        { value: 'title', name: 'По названию' },
      ],
    };
  },
  methods: {
    async fetchProjects() {
      try {
        this.isProjectsLoading = true;
        setTimeout(async () => {
          const res = await axios.get(
            'https://dev.aicap.tech/api/v1/interview/projects/'
          );
          this.projects = res.data.results;
          this.isProjectsLoading = false; // здесь из-за исп-я setTimeout
        }, 2000);
      } catch (err) {
        alert('problems');
      }
    },
    // ?
    createPost(projects) {
      console.log(projects);
      this.posts.push(projects); //добавление нового поста в массив posts
    },
  },
  mounted() {
    this.fetchProjects();
  },

  //   computed: {
  //     sortedProjects() {
  //     return [...this.project].sort((pro1, pro2) => {
  //         pro1[this.selectedPro]?.localeCompare(pro2[this.selectedPro]);
  //         },
  //             },
  //         },

  watch: {
    selectedPro(newValue) {
      console.log(newValue);
      this.projects.sort((pro1, pro2) => {
        return pro1[newValue]?.localeCompare(pro2[newValue]);
      });
    },
  },
};
</script>

<style>
.btn {
  display: flex;
  justify-content: space-between;
}
</style>
