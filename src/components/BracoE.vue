<template>
    
        <table>
            <hr><center>
              <h1>Braco Esquerdo</h1>
              <button @click="contrairCotovelo">Contrair o cotovelo esquerdo</button>
              <button @click="descontrairCotovelo">Descontrair o cotovelo esquerdo</button> 
              <h3>Status da contracao: {{statusCotovelo}}</h3>

              <button :disabled="desabilita" @click="rotacionarPulsoEsquerda">Rotacionar pulso esquerdo negativamente</button>
              <button :disabled="desabilita" @click="rotacionarPulsoDireita">Rotacionar pulso esquerdo positivamente</button> 
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
      this.status = 'Carregando...'
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

      this.status = 'Carregando...'
      axios
      .post('https://localhost:44390/DescontrairCotovelo', {status: this.statusCotovelo})
      .then(response => 
      {
        this.status = response.data.status;
        this.statusCotovelo = response.data.statusInterno;
      })
      .catch(error => {
        this.status = error;
      })
    },
    rotacionarPulsoDireita() {
      this.status = 'Carregando...'
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
      this.status = 'Carregando...'
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