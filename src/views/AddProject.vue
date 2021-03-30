<template>
  <div class="add-project">
    <ProjectForm use='add'/>
  </div>
</template>

<script>
import ProjectForm from '../components/ProjectForm.vue'

export default {
  components: { ProjectForm },
}
</script>