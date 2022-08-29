<template>
  <div class="home">
    <Herois :idHeroiAtual="idHeroiAtual"/>
  </div>
</template>

<script>

import NavBar from '../components/NavBar.vue'
import Herois from '../components/Herois.vue'

export default {
    name: 'HomeView',
    components: {
      NavBar,
      Herois
    },
    data() {
      return {
        idHeroiAtual: '1009610'
      }
    }
}
</script>

<style scoped>


</style>
