<script setup>
import { reactive } from "vue";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import TodoList from "./components/TodoList.vue";

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
    <Header :pending-tasks="getPendingTasks().length" />
    <Form
      :change-filter="(event) => (state.filter = event.target.value)"
      :temp-task="state.tempTask"
      :edit-temp-task="(event) => (state.tempTask = event.target.value)"
      :register-task="registerTasks"
    />
    <TodoList :tasks="getFilteredTasks()" />
  </div>
</template>
