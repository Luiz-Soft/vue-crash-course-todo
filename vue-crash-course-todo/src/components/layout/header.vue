<template>
  <header class="header">
    <h1>Immobile List</h1>
    <div id="nav"><router-link to="/">Home</router-link></div>
  </header>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  background: #333;
  color: #fff;
  text-align: center;
  padding: 10px;
}

.header a {
  color: #fff;
  padding-right: 5px;
}
</style>