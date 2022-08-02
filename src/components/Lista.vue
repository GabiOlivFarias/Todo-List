<template>
<div class="painel">
    <h2>{{ titulo }} </h2>
    <input type="text" class="filtro" v-on:keyup.enter="storeCheckbox" v-model="novoCheckbox" :key="checkbox.id" placeholder="Nova tarefa">
    <ul class="lista-checkbox">
        <li class="itens" v-for="checkbox in listaDeCheckbox" :key="checkbox.id">
        <p> <input type="checkbox" id="C1" /><label for="C1">{{ checkbox }} </label> 
        <button class="btn-apagar" @click="apagaTarefa"> </button> <!--apagar item-->
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
            checkbox: [],
            novoCheckbox: '',
        }
  },
    computed: {// capturou o input
      listaDeCheckbox() {
        return this.checkbox 
      },
    },
    methods: {//dispara o click

    setCheckbox(valor) {
        this.novoCheckbox = valor
    },
    storeCheckbox() {
        console.log(this.novoCheckbox)
        this.checkbox.push(this.novoCheckbox)
        this.setCheckbox('')
    },
    apagaTarefa() {
        console.log(this.novoCheckbox)
        this.checkbox.splice(this.novoCheckbox,1)
    }
    }
}
</script>
