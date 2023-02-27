<template>
<img src="./assets/cronometro.png" alt="">
<a class="timer">{{numero}}</a>

<div class="areaBtn">
  <button class="btn" @click="iniciar">{{botao}}</button>
  <button class="btn" @click="limpar">Limpar</button>
</div>

<div class="lista" v-show="historico.length > 0">
  <ul>
    <li v-for="item in historico" :key="item">Voce fez uma pausa em: {{item}}</li>
  </ul>
  <button @click="historico = []">Limpar histórico</button>
</div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      numero:0,
      botao: 'Iniciar',
      timer: null,
      segundos:0,
      minutos:0,
      horas:0,
      historico: []
    }
  },
  methods: {
    iniciar(){
      if(this.timer !== null){
        clearInterval(this.timer);
        this.timer = null;
        this.botao = 'Iniciar'
        if(this.segundos !== 0){
          this.historico.push(this.numero)
        }
      }else{
        this.timer = setInterval(()=>{
            this.rodarTimer()
        },1000);
        this.botao = 'Pausar'
      }
    },
    limpar(){
        if(this.timer !== null){
          clearInterval(this.timer);
          this.timer = null
        }
        this.segundos = 0
        this.minutos = 0
        this.horas = 0
        this.numero = 0
        this.botao = 'Iniciar'
        this.historico = []
    },
    rodarTimer(){
      this.segundos++;

      if(this.segundos == 59){
        this.segundos = 0;
        this.minutos++
      }

      if(this.minutos == 59){
        this.minutos = 0;
        this.horas++
      }

      let formato = (this.horas < 10 ? '0'+this.horas : this.horas) + ':'
      + (this.minutos < 10 ? '0'+this.minutos : this.minutos) + ','
      + (this.segundos < 10 ? '0'+this.segundos : this.segundos);

      return this.numero = formato
    }
  }
}
</script>

<style>
#app
{
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.img
{
  width: 420px;
  height: 420px;
  padding-top: 100px;
}

.timer
{
  color: #ffffff;
  font-size: 70px;
  margin: -280px;
}

.areaBtn
{
  margin-top: 495px;
  display: flex;
}
.btn
{
  -webkit-user-select: none;
  -moz-user-select: none;
  width: 150px;
  background-color: #fff;
  font-size: 20px;
  border: 0;
  border-radius: 5px;
  text-align: center;
  margin-left: 15px;
  margin-right: 15px;
  padding: 6px;
  cursor: pointer;
}

.btn:hover
{
  opacity: 0.8;
  transition: all 0.50s;
}

ul
{
  text-align: center;
  padding: 0;
}

ul li 
{
  margin-top: 4px;
  padding: 15px;
  background-color: rgb(70, 70, 70);
  list-style: none;
  color: #fff;
  font-size: 18px;
  border-radius: 6px;
}

.lista button
{
  cursor: pointer;
  border: 0;
  background-color: #fff;
  padding: 8px;
  border-radius: 5px;
  margin-bottom: 12px;
}
</style>
