<template>
  <div>
    <h1>Привет</h1>
    <div>
      <select-pro v-model="selectedPro" :options="sortOptions" />
      <project-form v-model="searchQuery" />
    </div>

    <projects-list :projects="forSearch" v-if="!isProjectsLoading" />
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
        // { value: 'title', name: 'По названию' },
      ],
      searchQuery: '',
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
  },
  mounted() {
    this.fetchProjects();
  },

  computed: {
    sortedProjects() {
      return [...this.projects].sort((pro1, pro2) => {
        return pro1[this.selectedPro]?.localeCompare(pro2[this.selectedPro]);
      });
    },
    forSearch() {
      return this.sortedProjects.filter((post) =>
        post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },

  //   watch: {
  //     selectedPro() {
  //       this.projects.sort((pro1, pro2) => {
  //         return pro1[this.selectedPro]?.localeCompare(pro2[this.selectedPro]);
  //       });
  //     },
  //     forSearch() {
  //       return this.selectedPro?.filter((proj) =>
  //         proj.title.includes(this.searchQuery)
  //       );
  //     },
  //   },
};
</script>

<style>
.btn {
  display: flex;
  justify-content: space-between;
}
</style>
