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

@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,700;1,800;1,900&display=swap');

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
}

.main__container{
  margin: 50px;
 height: auto;
}

h1{
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px ;
  color: #222;
}

</style>
