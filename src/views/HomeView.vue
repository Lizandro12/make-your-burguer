<template>
  <div>
      <Banner /> 
    <div class="main__container">
      <h1>Monte o seu Burguer:</h1>
      <BurgerForm /> 
    </div>
  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import BurgerForm from '../components/BurgerForm.vue'

export default {
  name: 'HomeView',
  components: {
    Banner,
    BurgerForm
  }
}
</script>
