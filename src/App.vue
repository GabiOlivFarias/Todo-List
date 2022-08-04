<template>
  <div>
    <div class="corpo">
      <h1 class="centraliza"> <img class="logo" :src="foto.url" :alt="foto.titulo"> </h1>
      <!--<h1> <img src="{{ foto.url }}" alt="{{ foto.titulo }}"></h1>
    somente com a linha acima não dá, tem q usar 'v-bind'
    v-bind:src="foto.url" ou só ':src="foto.url'-->
    </div>

    <!--pegando as tarefas digitadas no input-->
    <div class="input-lista">
      <input type="text" class="adicionaLista" v-model="lista" placeholder="Adicione uma nova lista">
      <button class="botao" @click="storeTodo"> </button>
      <button class="menu" @click="todasListas = !todasListas"> </button>
      <!--mudar nome depois, se não trava-->
      <div class="imagem-viking" v-show="visivel">
      <img src="../media/viking.png" alt="recado do viking">
      </div>

      <div class="tarefas" v-show="todasListas">
        <ul>
          <h2>Minhas Listas</h2>

          <div class="excluirListas">
            <input type="search" class="filtraLista" v-model="filtro" placeholder="Lista que deseja excluir">
            <button class="btn-excluirLista" @click="excluirLista(filtro)">Excluir lista</button>
          </div>

          <li class="itens" v-for="lista in conjuntoDelistas" :key="lista.id">
            <p>{{ lista }}</p>
          </li>
        </ul>
      </div>
    </div>

    <div class="tarefas">
      <ul class="lista-tarefa">
        <h1>Lista de tarefas</h1>
        <hr>
        <!-- <li class="lista-tarefa-itens" v-for="lista in conjuntoDelistas" :key="lista.id"></li> -->
        <Lista v-for="lista in conjuntoDelistas" :key="lista.id" :titulo="lista" />
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
    return {
      visivel: false, //para o recado viking

      foto: {
        url: 'https://jera.com.br/images/logo-facebook.png',
        titulo: 'logo Jera',
      },
      conjuntoDelistas: [],
      lista: '',
      filtro: '',

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
      var input = document.querySelector(".adicionaLista")
      var inputLista = document.querySelector(".input-lista") 
      if (this.lista == '') { // se lista estiver vazia, não inserir
        input.style.backgroundColor="#f8aaaad5"
        this.visivel = true

      } else {
        this.conjuntoDelistas.push(this.lista)
        this.lista = ''

        input.style.backgroundColor="#609175"
        this.visivel = false
        
      }
    },
    excluirLista(filtro) {
      var input = document.querySelector(".filtraLista")
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i'); // 'i' = tanto faz maiúsculo ou minúsculo e RegExp
                                              // varre as listas procurando a que tenha o texto do filtro
                                                                  // .trim faz ele ignorar espaços vazios.
        this.conjuntoDelistas.splice(this.conjuntoDelistas.indexOf(filtro), 1);

        input.style.backgroundColor="#7BAD85"
        this.filtro=''
      } else {
        // se o campo estiver vazio, não filtramos, retornamos a lista
        input.style.backgroundColor="#f8aaaad5"
      }
    }
  }
}
</script>

<style>
body {
  background-color: #1B494B;
}

p {
  font-size: 18pt;
}

ul h2, h1 {
  text-align: center;
  margin-bottom: 0;
  color:#0f3133;
}

hr {
  margin-top: 0;
}

ul {
  list-style: none;
}

input::placeholder {
  color: white;
}

.corpo {
  font-family: Helvetica, sans-serif;
  width: 96%;
  margin: auto;
}

.centraliza {
  text-align: center;
}

.logo {
  width: 15%;
  image-rendering: pixelated;
  float: right;
}

.input-lista {
  background-color: #1B494B;
  padding: 5px;
  margin: auto;
  border-radius: 10px;
  box-shadow: 2px 6px 2px 2px rgba(0, 0, 0, 0.541);
  width: 60%;
}

.adicionaLista {
  width: 60%;
  margin: auto 0 auto 150px;
  border: none;
  border-radius: 5px;
  padding: 5px;
  box-shadow: 2px 2ppx 2px rgba(0, 0, 0, 0.541);
  background-color: #93c59494;
  color: white;
}

.filtraLista {
  width:fit-content;
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.541);
  background-color: #93c59494;
  border-radius: 5px;
  padding: 5px;
  border: 1px #1B494B;
}

.botao, .menu {
  border-radius: 100px;
  padding: 15px;
  background-image: url("../media/icons8-adicionar-48.png ");
  background-size: 30px;
  background-position: center;
  background-repeat: no-repeat;
}
img{
  width: 200px;
  height: 200px;
   margin: auto;
  display: block;
}

.menu {
  background-image: url("../media/icons8-open-menu-48.png");
}

.botao:hover, .menu:hover {
  background-color: #61c578;
}

.tarefas {
  background-color: #93c594cc;
  padding: 20px;
  margin: 10px auto;
  border-radius: 10px;
  box-shadow: 3px 3px 3px black;
  max-width: 700px;
}

.add-tarefa {
  display: inline;
  border-radius: 100px;
  padding: 10px;
  background-image: url("../media/icons8-adicionar-48.png ");
  background-size: 20px;
  background-position: center;
  background-repeat: no-repeat;
}

/* aparencia de risco no item 'tarefa' */
input[type=checkbox]:checked~label {
  text-decoration: line-through;
  color: rgb(85, 85, 85);
}

.excluirListas {
  float: right;
  flex-direction: column;
}

.btn-apagarTarefa {
    border-radius: 100px;
    padding: 10px;
    background-image: url("../media/icons8-excluir-48.png");
    background-size: 20px;
    background-position: center;
    background-repeat: no-repeat;
}

.btn-apagarTarefa:hover {
  background-color: rgb(1, 153, 95);
}

.btn-excluirLista {
  margin-top: 5px;
  border-radius: 100px;
  font-family: Verdana, sans-serif;
  border-color: #0f3133;
  background-color: #93c594cc;
  color: white;
  width: fit-content;
}

.btn-excluirLista:hover {
  background-color: #0f3133;
}

</style>
