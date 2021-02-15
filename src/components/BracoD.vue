<template>
    
        <table>
            <hr><center>
              <h1>Braco Direito</h1>
              <button @click="contrairCotovelo">Contrair o cotovelo direito</button>
              <button @click="descontrairCotovelo">Descontrair o cotovelo direito</button> 
              <h3>Status da contracao: {{statusCotovelo}}</h3>

              <button :disabled="desabilita" @click="rotacionarPulsoEsquerda">Rotacionar pulso direito negativamente</button>
              <button :disabled="desabilita" @click="rotacionarPulsoDireita">Rotacionar pulso direito positivamente</button> 
              <h3>Status da rotacao: {{statusPulso}}</h3>
            </center>
            <hr>
        </table>
    
</template>

<script>

import axios from 'axios'
export default {
    data() {
        return {
            statusCotovelo: 'Em Repouso',
            statusPulso:'Em Repouso',            
            desabilita: true
        }
    },
    methods: {
    contrairCotovelo() {
                        
      axios
      .post('https://localhost:44390/ContrairCotovelo',{status: this.statusCotovelo})
      .then(response => 
      {
        this.status = response.data.status;
        this.statusCotovelo = response.data.statusInterno;
      })
      .catch(error => {
        this.status = error;
      })
      if(this.statusCotovelo=="Fortemente Contraido" || this.statusCotovelo=="Contraido")
        this.desabilita = false;
      else
        this.desabilita = true;
    },  
    descontrairCotovelo() {
      
      this.desabilita = true;          
      axios
      .post('https://localhost:44390/DescontrairCotovelo', {status: this.statusCotovelo})
      .then(response => 
      {
        this.status = response.data.status;
        this.statusCotovelo = response.data.statusInterno;
      })
      .catch( error => {
        this.status = error;
      })
    },
    rotacionarPulsoDireita() {
      
      axios
      .post('https://localhost:44390/RotacionarPulsoDireita',{status: this.statusPulso})
      .then(response => 
      {
        this.status = response.data.status;
        this.statusPulso = response.data.statusInterno;
      })
      .catch(error => {
        this.status = error;
      })
    },
    rotacionarPulsoEsquerda() {
      
      axios
      .post('https://localhost:44390/RotacionarPulsoEsquerda',{status: this.statusPulso})
      .then(response => 
      {
        this.status = response.data.status;
        this.statusPulso = response.data.statusInterno;
      })
      .catch(error => {
        this.status = error;
      })
    },  
    }
}
</script>

<style scoped>

</style>