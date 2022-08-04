<template>
<div class="painel">
    <h2>
        {{ titulo }} 
        <input type="text" class="filtro" v-on:keyup.enter="storeTarefa" v-model="novoTarefa" :key="tarefa.id" placeholder="Nova tarefa">
    </h2>
    <ul class="lista-tarefa">
        <li class="itens" v-for="tarefa in listaDetarefa" :key="tarefa">
        <div class="checkbox-lista"> <input type="checkbox" id="C1" />
            <label for="C1">{{ tarefa }} 
                <button class="btn-apagarTarefa" @click="apagaTarefa(tarefa)"></button> 
            </label> <!--apagar item-->
        </div>
        <!--no label foi aplicado com css a linha ao riscar o item-->
        </li>
    </ul>          
</div>
</template>

<script>
export default {
    name: 'lista',
    props: {
        titulo: String
    },
    data() {
        return{
            tarefa: [],
            novoTarefa: '',
        }
  },
    computed: {// capturou o input
      listaDetarefa() {
        return this.tarefa 
      },
    },
    methods: {//dispara o click

    setTarefa(valor) { //cria um valor do campo nova tarefa
        this.novoTarefa = valor
    },
    storeTarefa() {
        var input = document.querySelector(".filtro")
        if (this.novoTarefa == '') { // se lista estiver vazia, não inserir
      } else {
        this.tarefa.push(this.novoTarefa)
        this.setTarefa('') //define o valor como vazio após o enter
      }

        
    },
    
    apagaTarefa(tarefa) {
        console.log(tarefa)
        this.tarefa.splice(this.tarefa.indexOf(tarefa),1)

    }
    }
}
</script>

<style>

.painel {
    width: 100%;
    background-color: #1b494b8c;
    border-radius: 10px 10px 10px 10px;
}

.filtro {
    float: right;
    background-color: #1B494B;
    padding: 5px;
    margin-right: 5px;
    margin-top: 2px;
    border-radius: 8px;
    box-shadow: 2px 4px 2px 2px rgba(0, 0, 0, 0.541);
    width: 20%;
    color: white;
}

.checkbox-lista {
    font-family: Verdana, sans-serif;
    font-size: 15px;
    color:white;
    letter-spacing: 0.5px;
}

</style>
