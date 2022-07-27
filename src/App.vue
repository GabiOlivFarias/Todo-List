<template>
<div>
  <div class="corpo">
    <h1 class="centraliza"> <img class="logo" :src="foto.url" :alt="foto.titulo"> </h1>
    <!--<h1> <img src="{{ foto.url }}" alt="{{ foto.titulo }}"></h1>
    somente com a linha acima não dá, tem q usar 'v-bind'
    v-bind:src="foto.url" ou só ':src="foto.url'-->

  </div>
  
<!--pegando as tarefas digitadas no input-->
    <div class="input">
      <input type="text" class="filtro" v-model="digitado" placeholder="Adicione uma  nova lista">
      <button class="botao" @click="storeTodo"> </button>
    </div>


    <div class="tarefas">
    <ul class="lista-tarefa">
      <h2>Tarefas:</h2>
      <hr>
      <li class="lista-tarefa-itens" v-for="digitado in listaDeTarefas">
        <div class="painel">
          <h3>{{ digitado }} </h3>
          <input type="text" class="filtro" v-on:keyup.enter="storeCheckbox" v-model="novoCheckbox" placeholder="Novo checkbox">
          <ul class="lista-checkbox">
            <li class="itens" v-for="checkbox in listaDeCheckbox">
            <p>{{ checkbox }}</p>
            </li>
          </ul>          
        </div>
        
      </li>
    </ul>
  </div>

</div>
</template>

<script>
//import Vue from 'vue'

export default {
  data() {
 
    return{
      foto: {
        url: 'https://jera.com.br/images/logo-facebook.png',
        titulo:'logo Jera',
      },
      tarefas: [],
      digitado: '',
      checkbox: [],
      novoCheckbox: ''
      }
    },
    computed: {// capturou o input
      listaDeTarefas() {
          return this.tarefas
      },
      listaDeCheckbox() {
        return this.checkbox
      }
    },
    methods: {//dispara o click
      storeTodo() {
        this.tarefas.push(this.digitado)
        this.digitado = ''
      },
      storeCheckbox() {
        this.checkbox.push(this.novoCheckbox)
        this.novoCheckbox = ''   
      }
    
    }
    }
</script>

<style>
body{
  background-color: rgba(0, 0, 0, 0.699);
}
.corpo{
  font-family: Helvetica, sans-serif;
  width: 96%;
  margin: auto;
}
.centraliza{
  text-align: center;
}
.logo{
  width: 20%;
}
.input{
  background-color: #3f914079;
  padding: 20px;
  margin: auto;
  border-radius: 10px;
  box-shadow: 3px 3px 3px black;
  width: 700px;
}
input::placeholder{
  color: white;
}
.filtro{
  width: 60%;
  margin: auto 0 auto 200px;
  border-top: none;
  border-left: none;
  border-right: none;
  border-radius: 5px;
  padding: 5px;
  background-color: #3f9140b4;
}
.botao{
  border-radius: 100px;
  padding: 15px;
  background-image: url("../media/icons8-adicionar-48.png ");
  background-size: 30px;
  background-position: center;
  background-repeat: no-repeat;
}
.botao:hover{
  background-color: #55b86c;
}
.tarefas{
  background-color: #93c594cc;
  padding: 20px;
  margin: 10px auto;
  border-radius: 10px;
  box-shadow: 3px 3px 3px black;
  width: 700px;
}
ul h2{
  text-align: center;
  margin-bottom: 0;
}
hr{
  margin-top: 0;
}
.lista-tarefa{
  list-style: none;
}
.add-tarefa{
  display: inline;
  border-radius: 100px;
  padding: 10px;
  background-image: url("../media/icons8-adicionar-48.png ");
  background-size: 20px;
  background-position: center;
  background-repeat: no-repeat;
}

</style>
