<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/0.jpg">
      <center>
        <Cabeca/>
        <BracoE/>
        <BracoD/>
      </center>
    <hr>
  </div>
</template>

<script>
import Cabeca from './components/Cabeca.vue'
import BracoD from './components/BracoD.vue'
import BracoE from './components/BracoE.vue'
export default {
  name: 'App',
  components: {    
    Cabeca,
    BracoD,
    BracoE    
  }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
