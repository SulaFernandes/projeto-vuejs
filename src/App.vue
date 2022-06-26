<template>
  <div>
    <Navbar v-bind:logo="logo_src" v-bind:alt="app_name"/>
    <router-view/>
    <Footer/>
  </div>
</template>

<script>
  import Navbar from "./components/Navbar.vue"
  import Footer from "./components/Footer.vue"

  export default {

    components: {
      Navbar,
      Footer
    },
    data() {
      return {
        logo_src: "imagem/livros.png",
        app_name: "Listar livros"
      }
    }

  }
</script>
<style>

  * {
    font-family: Helvetica, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  .main-container {
    margin: 50px;
    min-height: 250px;
  }
  h3 {
    text-align: center;
    font-size: 30px;
    margin-bottom: 30px;
    color: #222;
  }

</style>
