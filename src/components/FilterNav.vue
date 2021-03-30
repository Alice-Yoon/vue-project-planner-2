<template>
  <div class="filter-nav">
    <button 
      v-for="btn in buttons" :key="btn.id"
      :class="{ active: currentFilter === btn.name }"
      @click="filterProjects(btn.name)" 
    >
      {{ btn.title }}
    </button>
  </div>
</template>

<script>
export default {
  props: ['currentFilter'],
  data() {
    return {
      buttons: [
        {
          id: 1,
          name: 'all',
          title: 'View All'
        },
        {
          id: 2,
          name: 'completed',
          title: 'Completed'
        },
        {
          id: 3,
          name: 'ongoing',
          title: 'Ongoing'
        }
      ]
    }
  },
  methods: {
    filterProjects(btnName) {
      this.$emit('filterProjects', btnName)
    }
  }
}
</script>

<style>
.filter-nav {
  /* border: 1px solid red; */
}
.filter-nav button {
  cursor: pointer;
  margin: 0 10px;
  text-transform: uppercase;
}
.filter-nav button.active {
  background-color: black;
  color: white;
}
</style>