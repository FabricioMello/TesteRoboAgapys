<template>
    
        <table>
            <hr>               
                  <center>
                    <h0>AGAPYS ROBO</h0>
                    <h1>Cabeca do Robo</h1>                                        
                    <button @click="inclinaCima">Subir Cabeca</button>                
                    <button @click="inclinaBaixo">Descer Cabeca</button>                            
                    <h3>Status da inclinacao: {{statusInclinacao}}</h3>                                       
                    <hr>
                    <button :disabled="desabilita" @click="rotacaoEsquerda">Rotacionar cabeca para esquerda</button>
                    <button :disabled="desabilita" @click="rotacaoDireita">Rotacionar cabeca para direita</button>
                    <h3>Status da rotacao: {{statusRotacao}}</h3>                   
                      
                  </center>         
            <hr>
        </table>
   
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            statusInclinacao: 'Em Repouso',
            statusRotacao:'Em Repouso',                        
            desabilita: false
        }
  },
  methods: {   
    
    inclinaCima() 
    {
      this.desabilita = false;
     
      this.status = 'Carregando...'
      axios
      .post('https://localhost:44390/InclinacaoCima',{status: this.statusInclinacao})
      .then(response => 
      {
        this.status = response.data.status
        this.statusInclinacao = response.data.statusInterno
        
      })
      .catch(error => {
        this.status = error;
      })
    },
  
    inclinaBaixo() {
    
      this.status = 'Carregando...'
      axios
      .post('https://localhost:44390/InclinacaoBaixo',{status: this.statusInclinacao})
      .then(response => 
      {
        this.status = response.data.status
        this.statusInclinacao = response.data.statusInterno
      })
      .catch(error => {
        this.status = error;
      })
      if(this.statusInclinacao=="Para Baixo" || this.statusInclinacao=="Em Repouso")
        this.desabilita = true;
      else
        this.desabilita = false;
    },
    rotacaoDireita() {
      this.status = 'Carregando...'
      axios
      .post('https://localhost:44390/RotacaoDireita',{status: this.statusRotacao})
      .then(response => 
      {
        this.status = response.data.status
        this.statusRotacao = response.data.statusInterno
      })
      .catch(error => {
        this.status = error;
      })
    },
    rotacaoEsquerda() {
      this.status = 'Carregando...'
      axios
      .post('https://localhost:44390/RotacaoEsquerda',{status: this.statusRotacao})
      .then(response => 
      {
        this.status = response.data.status
        this.statusRotacao = response.data.statusInterno
      })
      .catch(error => {
        this.status = error;
      })
    } 
}
}
</script>

<style scoped>

</style>