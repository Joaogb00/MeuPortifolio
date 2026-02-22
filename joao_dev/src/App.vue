<template>
  <Inicio/>
  <Footer/>
</template>

<script>
import Footer from './components/Footer.vue';
import Inicio from './components/Pages/Inicio.vue';

export default{
  name:'App',
  components:{
    Inicio,
    Footer
  }
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
}
body{
font-family: 'Roboto', sans-serif;
}
</style>