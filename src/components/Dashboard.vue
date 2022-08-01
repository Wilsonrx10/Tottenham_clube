<template>
 <div>
      <h1>Lista de Membros do Tottenham</h1>
   <mensagem :msg="msg"  v-show="msg" />
   <div class="membros">
     <div>
        <div id="membros-table-heading">
         <div class="order-id">#</div>
         <div>Nome:</div>
         <div>Email:</div>
         <div>Jogador Favorito</div>
         <div>Acoes:</div>
        </div>

        <div id="membros-table-row">
           <div class="membros-table-row" v-for="membro in membros" :key="membro.id">
            <div class="order-number">{{membro.id}}</div>
            <div>{{membro.nome}}</div>
            <div>{{membro.email}}</div>
            <div>{{membro.atleta}}</div>
            <div>
                <select name="status" class="status" @change="updateMembros($event, membro.id)">
                    <option value="">Seleciona</option>
                    <option :value="statu.tipo" v-for="statu in status" 
                    :key="statu.id" :selected="membro.status == statu.tipo">
                    {{statu.tipo}}
                    </option>
                </select>
                <button class="delete-btn" v-on:click="deleteMembros(membro.id)">Cancelar</button>
            </div>
           </div>
        </div>
     </div>
   </div>
 </div>
</template>

<script>
import mensagem from "../components/Mensagem.vue";
export default {
   name: "Dashboard",
   data:function() {
    return  {
        membros:null,
        membros_id:null,
        status:[],
        msg:null
    }
   },
   components:{
     mensagem
   },
   methods:{
    async getPedidos() {
        const req = await fetch("http://localhost:3000/membros");
        const data = await req.json();
        this.membros = data;
        // resgatar o status 
        this.getStatus();
    },
    async getStatus() {
        const req = await fetch("http://localhost:3000/status");
        const data = await req.json();
        this.status = data;
    },
    async deleteMembros(id) {

       const req = await fetch(`http://localhost:3000/membros/${id}`, {
        method: "DELETE"

      });

       this.getPedidos();

       // Mensagem 
       this.msg = "Membro eliminado com Sucesso";
       // Limpar mensagem 
       setTimeout(()=> this.msg = "", 5000);

    },

    async updateMembros(event, id) {

      const option = event.target.value;

      const dataJson = JSON.stringify({status:option});

      console.log(dataJson);

      const req = await fetch(`http://localhost:3000/membros/${id}`,{
       method:"PATCH",
       headers:{"content-type": "application/json"},
       body:dataJson
      });
      
      const res = await req.json();
       
       this.msg = `Membro Nª ${res.id} foi atualizado para ${res.status}`;
      
       setTimeout(()=> this.msg = "", 5000);

    }
   },
   mounted(){
     this.getPedidos();
   }
}
</script>

<style scoped>
   .membros {
    max-width: 1200px;
    margin: 0 auto;
  }
  #membros-table-heading,
  #membros-table-row,
  .membros-table-row {
    display: flex;
    flex-wrap: wrap;
  }
  #membros-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }
  .membros-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }
   #membros-table-heading div,
  .membros-table-row div {
    width: 22%;
  }
  #membros-table-heading .order-id,
  .membros-table-row .order-number {
    width: 5%;
  }
  select {
    padding: 12px 6px;
    margin-right: 12px;
  }
  .delete-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
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