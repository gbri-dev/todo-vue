<script setup>
const props = defineProps(['trocarFiltro'])
</script>
<template>
  <div class="container-fluid mb-4">  
    <div class="row justify-content-end">
      <div class="col-sm-2">
        <select class="form-select" @change="props.trocarFiltro">
          <option value="todas">Todas tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="concluidas">Concluídas</option>
        </select>    
      </div>  
    </div>            
  </div>
</template>
