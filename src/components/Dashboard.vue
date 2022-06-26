<template>
    <div id="livro-table">
        <Mensagem v-bind:mensagem="mensagem" v-show="mensagem"/>
        <div>
            <div id="livro-table-heading">
                <div class="livro-id">#</div>
                <div>Título:</div>
                <div>Autor:</div>
                <div>Volume:</div>
                <div>Quant. páginas:</div>
                <div>Ações:</div>
            </div>
        </div>
        <div id="livro-table-rows">
            <div class="livro-table-row" v-for="livro in livros" v-bind:key="livro.id">
                <div class="livro-number">{{ livro.id }}</div>
                <div>{{ livro.titulo }}</div>
                <div>{{ livro.autor }}</div>
                <div>{{ livro.volume }}</div>
                <div>{{ livro.qtdpaginas }}</div>
                <div>
                    <select name="stleitura" class="stleitura" @change="atualizarLivro($event, livro.id)">
                        <option value="">Status leitura</option>
                        <option v-for="status in stleitura" v-bind:key="status.id" v-bind:value="status.descricao" :selected="livro.stleitura == status.descricao">
                            {{ status.descricao }}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deletarLivro(livro.id)">Excluir</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import Mensagem from './Mensagem.vue'

export default {
    name: "Dashboard",
    components: {
        Mensagem
    },
    data() {
        return {
            livros: null, //livros cadastrados no BD
            livro_id: null,
            stleitura: [],
            mensagem: null
        }

    },
    methods: {
        async getLivros() {

            const requisicao = await fetch("http://localhost:3000/livros"); //faz requisição pra rota de livros cadastrados
            const data = await requisicao.json(); //converte os dados para json
            this.livros = data;
            
            this.getStatusLeitura();
        },
        async getStatusLeitura() {

            const req = await fetch("http://localhost:3000/stleitura");
            const data = await req.json();
            this.stleitura = data;

        },
        async deletarLivro(id) {
            
            const requisicao = await fetch(`http://localhost:3000/livros/${id}`, {
                method: "DELETE"
            });

            const res = await requisicao.json();

            //exibir msg
            this.mensagem = "Livro excluído com sucesso!";

            //limpar msg
            setTimeout(() => this.mensagem = "", 3000);

            this.getLivros();
        },
        async atualizarLivro(event, id) { //atualiza somente a propriedade stleitura
            
            const option = event.target.value;

            const dataJson = JSON.stringify({ stleitura: option });

            const requisicao = await fetch(`http://localhost:3000/livros/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await requisicao.json();

            //exibir msg
            this.mensagem = `Livro ${res.id} atualizado com sucesso!`;

            //limpar msg
            setTimeout(() => this.mensagem = "", 3000);
            
        }
    },
    mounted() {
        this.getLivros();
    }
}
</script>

<style scoped>

    #livro-table {
        max-width: 1200px;
        margin: 0 auto;
    }

    #livro-table-heading,
    #livro-table-rows,
    .livro-table-row {
        display: flex;
        flex-wrap: wrap;
    }

    #livro-table-heading {
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
    }

    #livro-table-heading div,
    .livro-table-row div {
        width: 19%;
    }

    .livro-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #CCC;
    }

    #livro-table-heading .livro-id,
    .livro-table-row .livro-number {
        width: 5%;
    }

    select {
        padding: 10px;
        margin-right: 12px;
    }

    .delete-btn {
        background-color: #d225f5;
        color:#222;
        font-weight: bold;
        border: 2px solid #222;
        padding: 8px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .delete-btn:hover {
        background-color: transparent;
        color: #222;
    }

</style>