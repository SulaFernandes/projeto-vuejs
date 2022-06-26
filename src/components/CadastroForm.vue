<template>
    <div>
        <Mensagem v-bind:mensagem="mensagem" v-show="mensagem"/>
        <div>
            <form id="cadastro-form" @submit="cadastrarLivro"> 
                <div class="input-container">
                    <label for="titulo">Título</label>
                    <input type="text" name="titulo" id="titulo" v-model="titulo">
                </div>
                <div class="input-container">
                    <label for="autor">Autor</label>
                   <input type="text" name="autor" id="autor" v-model="autor">
                </div>
                <div class="input-container">
                    <label for="volume">Volume</label>
                    <input type="text" name="volume" id="volume" v-model="volume">
                </div>
                <div class="input-container">
                    <label for="qtdpaginas">Quantidade de páginas</label>
                    <input type="text" name="qtdpaginas" id="qtdpaginas" v-model="qtdpaginas">
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Cadastrar">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Mensagem from './Mensagem.vue'
export default {
    name: "CadastroForm",
    components: {
        Mensagem
    },
    data() {
        return {
            
            //substitui null pelos dados obtidos na requisicao
            
            //dados preenchidos no form para enviar para o 'banco de dados(servidor)'
            titulo: null,
            autor: null,
            volume: null,
            qtdpaginas: null,
            //stleitura: "Não iniciada",
            mensagem: null,
        }
    },
    methods: {

        async cadastrarLivro(e) { //metodo ativado quando clicado no submit do form
            e.preventDefault();
            
            const data = {
                titulo: this.titulo, //dados vindo do data
                autor: this.autor,
                volume: this.volume,
                qtdpaginas: this.qtdpaginas,
                stleitura: "Não iniciada"
            }
            
            const dataJson = JSON.stringify(data) //converte data para texto
            //REQUISIÇÃO PARA SLAVAR OS DADOS NO BD
            const requisicao = await fetch("http://localhost:3000/livros", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await requisicao.json();

            //exibir msg
            this.mensagem = "Livro cadastrado com sucesso!";

            //limpar msg
            setTimeout(() => this.mensagem = "", 3000);
            
            //limpar campos
            this.titulo = " ",
            this.autor = " ",
            this.volume = " ",
            this.qtdpaginas = " "
        }
    },
    mounted() {
        //this.getBooks() //quando o componente form for inicializado ele chama getbooks
    }
}
</script>
<style scoped>

#cadastro-form {
    max-width: 400px;
    margin: 0 auto;
}
.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}
label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #d225f5;
}
input, select {
    padding: 5px 10px;
    width: 300px;
}
#stleitura-container {
    flex-direction: row;
    flex-wrap: wrap;
}
#stleitura-title {
    width: 100%;
}
.checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}
.checkbox-container span,
.checkbox-container input {
    width: auto;
}
.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
}
.submit-btn {
    background-color: #222;
    color:#d225f5;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin-right: 50px;
    cursor: pointer;
    transition: .5s;
}
.submit-btn:hover {
    background-color: transparent;
    color: #222;
}

</style>