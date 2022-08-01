<template>
<div id="main-banner">
    <h1>Tottenham Melhor Clube Inglês</h1>
</div>
</template>

<script>
export default {
  name:"Banner" 
}
</script>

<style scoped>

#main-banner {
 background-image: url('/public/images/time.png'); 
 background-position: 0 -100px;
 background-size: cover;
 height: 650px;
 display: flex;
 align-items: center;
 justify-content: flex-start;
}

#main-banner h1 {
    padding: 20px;
    color:#fff;
    text-align: center;
    font-size: 60px;
    background-color: rgb(11, 85, 222);
}
</style>
