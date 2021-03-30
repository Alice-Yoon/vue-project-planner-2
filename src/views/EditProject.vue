<template>
  <div class="edit-project">
    <ProjectForm
      use='edit'
      :id='this.id'
    />
  </div>
</template>

<script>
import ProjectForm from '../components/ProjectForm'

export default {
  props: ['id'],
  components: { ProjectForm },
}
</script>