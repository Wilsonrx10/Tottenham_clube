<template>
  <div class="main-container">
    <h2>Testando Parametros na rota</h2>
    <h1>{{ $route.params.divisao }}</h1>
  </div>
</template>

<script>
  export default {
    name: "Elencos",
    data:function(){
      return  {
        logado: true
      }
    },
    methods: {
      Rederecinar() {
        if (this.logado == false) {
          this.$router.push({name: 'home'});
        }
      }
    },
    mounted:function() {
      this.Rederecinar();
    }
  }
</script>