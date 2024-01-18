<script setup>
const props = defineProps(['trocarFiltro'])
</script>
<template>  
  <div class="row justify-content-end">
    <div class="col-sm-3">
      <div class="input-group mb-3">
        <label class="input-group-text" for="filtrarTarefas">Filtrar</label>
        <select id="filtrarTarefas" class="form-select" @change="props.trocarFiltro">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="concluidas">Concluídas</option>
        </select>    
      </div>
    </div>  
  </div>              
</template>
