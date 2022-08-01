<template>
<div>
    <mensagem :msg="msg"  v-show="msg" />
    <div id="formulario">
        <h2>{{version}}</h2>
        <form @submit="Addmembros">
            <input type="text" name="nome" id="nome" v-model="nome" placeholder="digita seu nome"> <br>

            <input type="text" name="email" id="email" v-model="email" placeholder="digita seu email"> <br>

            <select v-model="atleta">
                <option value="" selected>Seleciona teu jogador favorito</option>
                <option v-for="atleta in atletas" :key="atleta.id" :value="atleta.nome">{{ atleta.nome }}</option>
            </select> <br>

            <button>Fazer o Cadastro</button>
        </form>
    </div>
</div>
</template>

<script>
import {mapState} from 'vuex'
import mensagem from './Mensagem.vue'
export default {
    name: "Form_membro",
    components:{
     mensagem
    },  
    data:function() {
        return {
        nome: null,
        email: null,
        atleta: null,
        atletas: null,
        msg: null,
        }
    },
    methods: {
        async getAtletas() {

            const req = await fetch("http://localhost:3000/Jogadores");

            const data = await req.json();

            this.atletas = data.atletas;

            console.log(data);

        },
        async Addmembros(e) {

            e.preventDefault();

            const data = {
                nome: this.nome,
                email: this.email,
                atleta: this.atleta,
                status: "pendente"
            }

            const datajson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/membros", {
                method:"POST",
                headers: {"content-type:": "application/json"},
                body: datajson
            });

            const resultado = await req.json();


            console.log(resultado);

           // colocar mensagens no Sistema 

           this.msg = "Novo Adepto do Tottenham Cadastrado com Sucesso";

           // Limpar os campos 

           this.nome = ""
           this.email = ""

           // Limpar mensagem 
           setTimeout(()=> this.msg = "", 3000);

        }
    },
    mounted: function () {
        this.getAtletas();
    }
}
</script>


<style scoped>
#formulario {
    margin: 0 auto;
    justify-content: center;
    text-align: center;
    align-items: center;
    background-color: #ddd;
    width: 650px;
    padding: 40px;
}

#formulario input,
select {
    padding: 10px;
    width: 100%;
    border: none;
    outline: 0;
    border-bottom: 4px solid #ddd;
    margin: 10px;
}

#formulario button {
    width: 300px;
    background-color: rgb(11, 85, 222);
    padding: 15px;
    border: 1px solid rgb(11, 85, 222);
    border-radius: 30px;
    color: white;
    cursor: pointer;
}
</style>
