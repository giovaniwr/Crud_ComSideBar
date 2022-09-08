<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form id="formulario-form" @submit="createCadastro">
                <div class="input-container">
                    <label for="nome">Nome:</label>
                    <input type="text" id="nome" v-model="nome" placeholder="Digite o seu nome"/>
                </div>
                <div class="input-container">
                    <label for="cpf">CPF:</label>
                    <input type="text" id="cpf" v-model="cpf" placeholder="Digite o seu CPF"/>
                </div>
                <div class="input-container">
                    <label for="telefone">Telefone:</label>
                    <input type="text" id="telefone" v-model="telefone" placeholder="Digite o seu Telefone"/>
                </div>
                <div class="input-container">
                    <label for="nome">Email:</label>
                    <input type="text" id="email" v-model="email" placeholder="Digite o seu Email"/>
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Salvar"/>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue';
    

    export default {
    name: "Formulrio",
    data() {
        return {
            nome: null,
            cpf: null,
            telefone: null,
            email: null,
            msg: null,
        };
    },
    methods: {
        async createCadastro(e) {
            e.preventDefault();
            const data = {
                nome: this.nome,
                cpf: this.cpf,
                telefone: this.telefone,
                email: this.email,
            };
            const dataJson = JSON.stringify(data);
            const req = await fetch("http://localhost:3000/cadastros", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });
            const res = await req.json();

            //cadastroo mensagem
            this.msg = `Cadastro Nº ${res.id} realizado com sucesso!`;

            //limpar mensagem
            setTimeout(() => this.msg = "", 3000);

            //limpar os campos
            this.nome = "";
            this.cpf = "";
            this.telefone = "";
            this.email = "";
        }
    },
    components: {
    Message,
}
}
</script>

<style scoped>
    #formulario-form {
        max-width: 400px;
        margin: 0 auto;
    }
    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
       
    }
    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }
    input{
        padding: 5px 10px;
        width: 400px;
    }
    .submit-btn{
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding:10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }
    .submit-btn:hover {
        background-color: transparent;
        color: #222;
    }


</style>