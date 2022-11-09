<template>
<div>
  <ButtonComponent/>
</div>
</template>

<script>
import ButtonComponent from './components/ButtonComponent.vue'

export default {
  name: 'App',
  components: {
    ButtonComponent
  },
  
  
}
</script>

<style>
body{
  background-color: #006C99;
 /* background-image: url("https://diegomonfort.com/muestras/doggies/fondo2b.jpg");*/
  font-family: Montserrat, sans-serif;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
  margin: 40px;
}


</style>
