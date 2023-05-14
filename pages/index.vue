<template>
  <div class="home-page">
    <nav class="navbar">
      <router-link to="/">Strona główna</router-link>
      <router-link to="/gallery">Galeria</router-link>
    </nav>
    <h1>Witaj w mojej galeri w VUE</h1>
    <router-link to="/gallery">Przejdź do galeri</router-link>
  </div>
</template>

<script>
export default {
  name: 'HomePage'
}
</script>

<style scoped>
.home-page {
  background-color: #f5f5f5;
  padding: 20px;
}

.navbar {
  background-color: #333;
  color: #fff;
  display: flex;
  justify-content: space-between;
  padding: 10px;
}

.navbar a {
  color: #fff;
  text-decoration: none;
  margin: 0 10px;
}

.navbar a:hover {
  text-decoration: underline;
}
</style>
