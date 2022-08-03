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
    <input type="text" class="filtro" v-model="lista" placeholder="Adicione uma nova lista">
    <button class="botao" @click="storeTodo"> </button>
      <button class="menu" @click="todasListas = !todasListas"> </button> <!--mudar nome depois, se não trava-->

      <div class="tarefas" v-show="todasListas">
      <ul>
        <h2>Minhas Listas</h2>
        <li class="itens" v-for="lista in conjuntoDelistas" :key="lista.id">
        <p> {{ lista }}</p>
        </li>
      </ul>
      </div>
  </div>

    <div class="tarefas">
      <ul class="lista-tarefa">
        <h1>Lista de tarefas:</h1>
        <hr>
        <!-- <li class="lista-tarefa-itens" v-for="lista in conjuntoDelistas" :key="lista.id"></li> -->
        <Lista v-for="lista in conjuntoDelistas" :key="lista.id" :titulo="lista"/> 
      </ul>
    </div>

</div>
</template>

<script>
import Lista from './components/Lista.vue'

export default {
  components: {
    Lista
  },
  data() {
    return{
      foto: {
        url: 'https://jera.com.br/images/logo-facebook.png',
        titulo:'logo Jera',
      },
      conjuntoDelistas: [],
      lista: '',

      todasListas: false//aqui faz o menu esconder no começo
      }
    },
    computed: {// capturou o input
      listaDeTarefas() {
          return this.conjuntoDelistas
      }
    },
    methods: {//dispara o click
      storeTodo() {
        this.conjuntoDelistas.push(this.lista)
        this.lista = ''
      }
    }
    }
</script>

<style>
body{
  background-color: rgba(236, 14, 14, 0.699);
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
  margin: auto 0 auto 150px;
  border-top: none;
  border-left: none;
  border-right: none;
  border-radius: 5px;
  padding: 5px;
  background-color: #3f9140b4;
}
.botao, .menu{
  border-radius: 100px;
  padding: 15px;
  background-image: url("../media/icons8-adicionar-48.png ");
  background-size: 30px;
  background-position: center;
  background-repeat: no-repeat;
}
.menu{
  background-image: url("../media/icons8-open-menu-48.png");
}
.botao:hover, .menu:hover{
  background-color: #55b86c;
}
.tarefas{
  background-color: #93c594cc;
  padding: 20px;
  margin: 10px auto;
  border-radius: 10px;
  box-shadow: 3px 3px 3px black;
  max-width: 700px;
}
ul h2, h1{
  text-align: center;
  margin-bottom: 0;
}
hr{
  margin-top: 0;
}
ul{
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
/* aparencia de risco no item 'tarefa' */
input[type=checkbox]:checked ~ label {
   text-decoration: line-through;
   color: rgb(85, 85, 85);
}
.btn-apagar{
  border-radius: 100px;
  padding: 10px;
  background-image: url("../media/icons8-excluir-48.png");
  background-size: 20px;
  background-position: center;
  background-repeat: no-repeat;
}
p{
  font-size: 18pt;
}
</style>
