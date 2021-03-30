<template>
  <div class="single-project" :class="project.complete ? 'complete': 'incomplete'">
    <div class="title-section">
      <h2 @click="toggleDetails">{{ title }}</h2>
      <div class="icons">
        <span @click="editProject" class="material-icons">edit</span>
        <span @click="deleteProject" class="material-icons">delete</span>
        <span @click="toggleDone" class="material-icons">done</span>
      </div>
    </div>
    <div v-if="detailsShow" class="details-section">
      <p>{{ details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['project'],
  data() {
    return {
      title: '',
      details: '',
      detailsShow: false,
      uri: `http://localhost:3000/projects/${this.project.id}`
    }
  },
  mounted() {
    this.title = this.project.title
    this.details = this.project.details
  },
  methods: {
    toggleDetails() {
      this.detailsShow = !this.detailsShow
    },
    editProject() {
      this.$router.push(`/projects/edit/${this.project.id}`)
    },
    deleteProject() {
      console.log("deleteProject", this.project.id)
      fetch(this.uri, { method: 'DELETE' })
        .then(() => {
          this.$emit('delete', this.project.id)
        })
        .catch(err => console.log(err))
    },
    toggleDone() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type' : 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete })
      })
        .then(() => {
          this.$emit('toggleDone', this.project.id)
        })
        .catch(err => console.log(err))
    }
  }
}
</script>

<style>
.single-project {
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
  width: 650px;
  margin: 20px auto;
  padding: 10px 20px;
}
.single-project.complete {
  border-left: 4px solid green;
}
.single-project.incomplete {
  border-left: 4px solid crimson;
}
.title-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.title-section h2 {
  cursor: pointer;
}
.material-icons {
  cursor: pointer;
  margin: 0 5px;
}
.details-section {
  text-align: start
}
</style>