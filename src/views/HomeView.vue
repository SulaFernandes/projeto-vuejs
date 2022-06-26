<template>
  <div>
    <Banner />
    <div class="main-container">
      <h3>Cadastrar livro:</h3>
      <CadastroForm />
    </div>
  </div>
</template>

<script>
import Banner from '../components/Banner'
import CadastroForm from '../components/CadastroForm'

export default {
  name: 'Home',
  components: {
    Banner,
    CadastroForm
  }
}
</script>
