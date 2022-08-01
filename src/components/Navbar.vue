<template>
  <div id="nav">
      <router-link to="/" id="logo_url">
        <img :src="logo" alt="" id="logo" />
      </router-link>
      <router-link to="/">Página Inicial</router-link>
      <router-link to="/pedidos">Pedidos</router-link> 
      <router-link :to="{name:'Elencos', params: {divisao:'sub21'}}">Elencos da Equipa</router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: ["logo"],
};
</script>

<style scoped>
#nav {
  background-color: black;
  border-bottom: 4px solid black;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

#nav #logo_url {
  margin: auto;
  margin-left: 0;
}
#logo {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}
#nav a {
    color:white;
    text-decoration: none;
    margin:5px;
    transition: .5s;
    font-size: 18px;
}
#nav a:hover {
  color:rgb(11, 85, 222);
}
</style>
