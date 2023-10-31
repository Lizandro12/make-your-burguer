<template>
  <nav id="nav">
    <router-link to="/" id="logo__url">
    <img :src="logo" :alt="alt" id="logo">
    </router-link>
    <router-link to="/" class="nav__link">Página Inicial</router-link> 
    <router-link to="/pedidos" class="nav__link">Pedidos</router-link>
  </nav>
</template>

<script>

export default {
    name: "NavigationBar",
    props: ["logo", "alt"]
}

</script>

<style scoped>

#nav{
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
}

#logo__url{
    margin: auto;
    margin-left: 0;
}

#logo{
    width: 40px;
    height: 40px;
}

#nav .nav__link{
    color: #fcba03;
    text-decoration: none;
    margin: 12px;
    transition: 0.5s;
}

#nav .nav__link:hover{
    color: #ffffff;
}
</style>