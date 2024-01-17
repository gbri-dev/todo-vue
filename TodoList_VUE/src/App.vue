<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import FiltraItem from './components/FiltraItem.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

const estadoApp = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      concluido: false
    },
    {
      titulo: 'Estudar SASS',
      concluido: false
    },
    {
      titulo: 'Fazer caminhada e corrida',
      concluido: true
    }
  ]
})

const getTarefasPendentes = () => {
  return estadoApp.tarefas.filter(tarefa => !tarefa.concluido)
}

const getTarefasConcluidas = () => {
  return estadoApp.tarefas.filter(tarefa => tarefa.concluido)
}

const getTarefasFiltradas = () => {
  const { filtro } = estadoApp

  switch(filtro){
    case 'pendentes':      
      return getTarefasPendentes();
    case 'concluidas':
      return getTarefasConcluidas();
      default: 
      return estadoApp.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estadoApp.tarefaTemp,
    finalizada: false
  }
  estadoApp.tarefas.push(tarefaNova);
  estadoApp.tarefaTemp = '';
  document.querySelector('input').value = ''
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <FiltraItem :trocar-filtro="evento => estadoApp.filtro = evento.target.value" />
    <Formulario :cadastra-tarefa="cadastraTarefa" :tarefa-temp="estadoApp.tarefaTemp" :push-tarefa-temp="evento => estadoApp.tarefaTemp = evento.target.value" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
