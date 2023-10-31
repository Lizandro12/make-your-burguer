<template>
  <div>
    <NavigationBar :logo="logo_src" :alt="app_name"/>
    <router-view/>
    <RodaPe/>
  </div>
</template>


<script>

import NavigationBar from './components/NavigationBar.vue';
import RodaPe from './components/RodaPe.vue';

  export default {
    name: 'App',
    components: {
      NavigationBar,
      RodaPe
    },
    data () {
      return {
        logo_src: "/img/logo.png",
        app_name: "Make Your Gurguer"
      }
    }
  }

</script>
<style>

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, Helvetica, sans-serif;
}

.main__container{
  margin: 50px;
 height: 100vh;
}

h1{
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px ;
  color: #222;
}

</style>
