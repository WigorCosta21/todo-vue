<script setup>
import { reactive } from "vue";

const state = reactive({
  filter: "all",
  tempTask: "",
  tasks: [
    {
      title: "Estudar ES6",
      fineshed: false,
    },
    {
      title: "Estudar SASS",
      fineshed: false,
    },
    {
      title: "Ir para academia",
      fineshed: true,
    },
  ],
});

const getPendingTasks = () => state.tasks.filter((task) => !task.fineshed);

const getFinishedTasks = () => state.tasks.filter((task) => task.fineshed);

const getFilteredTasks = () => {
  const { filter } = state;

  switch (filter) {
    case "pending":
      return getPendingTasks();
    case "finished":
      return getFinishedTasks();
    default:
      return state.tasks;
  }
};

const registerTasks = () => {
  const newTask = {
    title: state.tempTask,
    fineshed: false,
  };

  state.tasks.push(newTask);
  state.tempTask = "";
};
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui {{ getPendingTasks().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="registerTasks">
      <div class="row">
        <div class="col">
          <input
            :value="state.tempTask"
            required
            type="text"
            placeholder="Digite sua tarefa"
            class="form-control"
            @change="(event) => (state.tempTask = event.target.value)"
          />
        </div>
        <div class="col-md-1">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select
            @change="(event) => (state.filter = event.target.value)"
            class="form-control"
          >
            <option value="all">Todas Tarefas</option>
            <option value="pending">Tarefas Pendentes</option>
            <option value="finished">Tarefas Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getFilteredTasks()">
        <input
          @change="(event) => (task.fineshed = event.target.checked)"
          :checked="task.fineshed"
          :id="task.title"
          type="checkbox"
        />
        <label
          :class="{ done: task.fineshed === true }"
          class="ms-3"
          for="task.title"
          >{{ task.title }}</label
        >
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
