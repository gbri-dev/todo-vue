<script setup>
  const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'pushTarefaTemp'])
</script>
<template>
  <form @submit.prevent="props.cadastraTarefa">
    <div class="row">
      <div class="col-sm-10 mb-4">
        <input @value="props.tarefaTemp" @change="props.pushTarefaTemp" type="text" class="form-control" placeholder="Digite sua tarefa aqui..." required />
      </div>
      <div class="col-sm-2 mb-4">
        <button type="submit" class="btn btn-outline-primary w-100">Cadastrar</button>
      </div>      
    </div>
  </form>
</template>