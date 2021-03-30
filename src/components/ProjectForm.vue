<template>
  <div class="project-form">
    <form @submit.prevent='submitHandler'>
      <label>Title:</label>
      <input v-model="title" type="text" required>
      <label>Details:</label>
      <textarea v-model="details" required></textarea>
      <button>Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ['use', 'id'],
  data() {
    return {
      title: '',
      details: '',
      complete: false,
      uri: 'http://localhost:3000/projects'
    }
  },
  mounted() {
    if(this.use === 'add') return
    fetch(`http://localhost:3000/projects/${this.id}`)
        .then(res => res.json())
        .then(data => {
          this.title = data.title
          this.details = data.details
          this.complete = data.complete
        })
        .catch(err => console.log(err))
  },
  methods: {
    submitHandler() {
      const project = {
        title: this.title,
        details: this.details,
        complete: this.complete
      }  

      if(this.use === 'add') {
        fetch(this.uri, {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(project)
        })
        .then(() => this.$router.push('/'))
        .catch(err => console.log(err))

      } else {
        fetch(this.uri + `/${this.id}`, {
          method: 'PATCH',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(project)
        })
        .then(() => this.$router.push('/'))
        .catch(err => console.log(err))
      }
    }
  }
}
</script>

<style>
form {
    background: white;
    padding: 20px;
    border-radius: 10px;
    width: 75%;
    margin: 10px auto;
  }
  label {
    display: block;
    color: #bbb;
    text-transform: uppercase;
    font-size: 14px;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
  }
  input {
    padding: 10px;
    border: 0;
    border-bottom: 1px solid #ddd;
    width: 100%;
    box-sizing: border-box;
  }
  textarea {
    border: 1px solid #ddd;
    padding: 10px;
    width: 100%;
    box-sizing: border-box;
    height: 100px;
  }
  form button {
    display: block;
    margin: 20px auto 0;
    background: #00ce89;
    color: white;
    padding: 10px;
    border: 0;
    border-radius: 6px;
    font-size: 16px;
    cursor: pointer;
  }
</style>