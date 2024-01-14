<script setup>
import { reactive } from 'vue';

const estadoApp = reactive({
  tarefaTemp: '',
  filtro: 'todas',
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
  estadoApp.tarefas.push(tarefaNova)
  estadoApp.tarefaTemp = ''
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>

  <form @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col-sm mb-4">
        <input @value="evento.tarefaTemp" @change="evento => evento.tarefaTemp = evento.target.value" type="text" class="form-control" placeholder="Digite sua tarefa aqui...">
      </div>
      <div class="col-sm-1 mb-4">
        <button  type="submit" class="btn btn-primary">Cadastrar</button>
      </div>
      <div class="col-sm-2">
        <select class="form-control" @change="evento => estadoApp.filtro = evento.target.value">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="concluidas">Concluídas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
      <input type="checkbox" :checked="tarefa.concluido" :id="tarefa.titulo" @change="evento => tarefa.concluido = evento.target.checked">
      <label :for="tarefa.titulo" class="ms-3" :class="{ done: tarefa.concluido}">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
</div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
