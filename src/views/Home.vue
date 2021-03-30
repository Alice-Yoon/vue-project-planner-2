<template>
  <div class="home">
    <FilterNav />
    <div v-for="project in projects" :key="project.id">
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
      projects: []
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => {
        console.log("DATA!!", data)
        this.projects = data
      })
      .catch(err => console.log(err))
  }
}
</script>
