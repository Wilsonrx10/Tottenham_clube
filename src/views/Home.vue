<template>
  <div>
    <Banner />
    <div class="main-container">
      <h1>Formulário de Inscrição</h1>
      <Form_membro/>
    </div>
  </div>
</template>

<script>
import Banner from "../components/Banner.vue";
import Form_membro from "../components/Form_membro.vue";
export default {
  name: "Home",
  components:{
    Banner,
    Form_membro
  }
}
</script>
