<template>
  <div id="main-banner">
    <h1>Lista de livros</h1>
  </div>
</template>

<script>
  export default {
    name: "Banner"
  }
</script>

<style scoped>
  #main-banner {
    background-image: url('/public/imagem/books.jpg');
    background-position: 0 -250px;
    background-size: cover;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }
  #main-banner h1 {
    color: #ffffff;
    text-align: center;
    font-size: 30px;
    padding: 20px 40px;
  }
</style>