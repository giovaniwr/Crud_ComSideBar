<template>
    <div id="cadastro-table">
        <div>
            <div id="cadastro-table-heading">
                <div class="order-id">#:</div>
                <div>Nome:</div>
                <div>CPF:</div>
                <div>Telefone:</div>
                <div>Email:</div>
                <div>Ações:</div>
            </div>
        </div>
        <div id="cadastro-table-rows">
            <div class="cadastro-table-row" v-for="cadastro in cadastros" :key="cadastro.id">
                <div class="order-number">{{ cadastro.id }}</div>
                <div>{{ cadastro.nome }}</div>
                <div>{{ cadastro.cpf }}</div>
                <div>{{ cadastro.telefone }}</div>
                <div>{{ cadastro.email }}</div>
                <div>
                    <button class="edit-btn" @click="editCadastro(cadastro.id)">Editar</button>
                    <button class="delete-btn" @click="deleteCadastro(cadastro.id)">Deletar</button>
                </div>
            </div>
        </div>
    </div> 
</template>

<script>
    export default {
        name: "Dashboard",
        data() {
            return {
                cadastros: null,
                cadastro_id: null
            }
        },
        methods: {
            async getCadastro() {
                const req = await fetch("http://localhost:3000/cadastros");

                const data = await req.json();

                this.cadastros = data;
            
                console.log(this.cadastros);
            },
            async editCadastro(event, id) {
                const option = event.target.value;
                
                const dataJson = JSON.stringify({status: option});

                const req = await fetch("http://localhost:3000/cadastros", {
                    method: "PACH",
                    headers: { "Content-Type": "application/json"},
                    body: dataJson
                })

                const res = await req.json();
            },
            async deleteCadastro(id) {
                const req = await fetch(`http://localhost:3000/cadastros/${id}`,
                {
                    method: "DELETE"
                });
                const res = await req.json();

                this.getCadastro();
            }
        },
        mounted() {
            this.getCadastro();
        }
    }
</script>
<style scoped>
    #cadastro-table {
        max-width: 1200px;
        margin:0 auto;
    }
    #cadastro-table-heading,
    #cadastro-table-rows, 
    .cadastro-table-row {
        display: flex;
        flex-wrap: wrap;
    }
    #cadastro-table-heading{
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
    }
    #cadastro-table-heading div,
    .cadastro-table-row div {
        width: 19%;
    }
    .cadastro-table-row {
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #CCC;
    }
    #cadastro-table-heading .order-id,
    .cadastro-table-row .order-number {
        width: 5%;
    }
    .edit-btn {
        background-color: #007bff ;
        color: #FFF;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }
    .edit-btn:hover{
        background-color: transparent;
        color: #222;

    }
    .delete-btn {
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }
    .delete-btn:hover{
        background-color: transparent;
        color: #222;

    }


</style>