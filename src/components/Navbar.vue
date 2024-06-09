<template>
  <div class="navbar">
    <router-link to="/">Projects</router-link>
    <router-link :to="{name:'addProject'}">Add Project</router-link>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.navbar{
    text-align: center;
    margin: 40px auto;
}
.navbar a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;
}
a.router-link-active{
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
}
</style>