<template>
  <nav class="nav-bar">
    <router-link :to="{name : 'Home' }">Projects</router-link>
    <router-link :to="{name : 'AddProject' }">Add a new Project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
.nav-bar {
  margin-bottom: 25px;
}
.nav-bar a {
  text-decoration: none;
  color: #999;
  font-size: 18px;
  margin: 0 10px;
}
a.router-link-active {
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
}
</style>