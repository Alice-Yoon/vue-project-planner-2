<template>
  <div class="home">
    <FilterNav :currentFilter='currentFilter' @filterProjects='filteredProjectsHandler' />
    <div v-for="project in filteredProjects" :key="project.id">
      <SingleProject :project='project' />
    </div>
  </div>
</template>

<script>
import FilterNav from '../components/FilterNav.vue'
import SingleProject from '../components/SingleProject.vue'

export default {
  name: 'Home',
  components: { FilterNav, SingleProject },
  data() {
    return {
      projects: [],
      currentFilter: 'all'
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => {
        this.projects = data
      })
      .catch(err => console.log(err))
  },
  computed: {
    filteredProjects() {
      if(this.currentFilter === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      if(this.currentFilter === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  },
  methods: {
    filteredProjectsHandler(btnName) {
      this.currentFilter = btnName
    }
  }
}
</script>
