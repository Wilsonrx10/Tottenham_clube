<template>
  <div class="container-mensagem">
    <p>{{msg}}</p>
  </div>
</template>

<script>
export default {
   name:"mensagem",
   props: ["msg"]
}
</script>

<style scoped>
   .container-mensagem {
     color:#004085;
     background-color: #CCE5FF;
     border:2px solid #88DAFF;
     border-radius: 5px;
     padding: 10px;
     max-width: 400px;
     margin:30px auto;
   }
</style>