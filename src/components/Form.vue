<script setup>
const props = defineProps([
  "registerTask",
  "tempTask",
  "changeFilter",
  "EditTempTask",
]);
</script>

<template>
  <form @submit.prevent="props.registerTask">
    <div class="row">
      <div class="col">
        <input
          :value="props.tempTask"
          required
          type="text"
          placeholder="Digite sua tarefa"
          class="form-control"
          @change="props.EditTempTask"
        />
      </div>
      <div class="col-md-1">
        <button class="btn btn-primary" type="submit">Cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="props.changeFilter" class="form-control">
          <option value="all">Todas Tarefas</option>
          <option value="pending">Tarefas Pendentes</option>
          <option value="finished">Tarefas Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
