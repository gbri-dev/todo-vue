<script setup>
  const props = defineProps(['tarefasPendentes'])
</script>
<template>
  <header class="badge bg-dark p-5 mb-4 mt-4 rounded-3 w-100">
      <h1>Minhas tarefas</h1>
      <h3 v-if="props.tarefasPendentes > 0">Você possui {{ props.tarefasPendentes }} tarefas pendentes</h3>
      <h3 v-else><i class="bi bi-emoji-sunglasses"></i>Parabéns, você finalizou todas as tarefas!</h3>
  </header>
</template>
