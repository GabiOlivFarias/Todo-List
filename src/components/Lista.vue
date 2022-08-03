<template>
<div class="painel">
    <h2>{{ titulo }} </h2>
    <input type="text" class="filtro" v-on:keyup.enter="storetarefa" v-model="novoTarefa" :key="tarefa.id" placeholder="Nova tarefa">
    <ul class="lista-tarefa">
        <li class="itens" v-for="tarefa in listaDetarefa" :key="tarefa">
        <p> <input type="checkbox" id="C1" /><label for="C1">{{ tarefa }} 
        <button class="btn-apagar" @click="apagaTarefa(tarefa)"> </button> </label> <!--apagar item-->
        </p>
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
    storetarefa() {
        this.tarefa.push(this.novoTarefa)
        this.setTarefa('') //define o valor como vazio após o enter
    },
    
    apagaTarefa(tarefa) {
        console.log(tarefa)
        this.tarefa.splice(this.tarefa.indexOf(tarefa),1)

    }
    }
}
</script>
