<script setup>
import { reactive, computed } from 'vue';
import TaskHeader from './components/TaskHeader.vue';
import Form from './components/Form.vue';
import TaskList from './components/TaskList.vue';

const state = reactive({
  filter: "All Tasks",
  taskTemp: '',
  tasks: []
});

const changeFilter = (event) => { state.filter = event.target.value };

const getTaskToDo = () => {
  return state.tasks.filter(task => !task.finished);
};

const getTaskFinished = () => {
  return state.tasks.filter(task => task.finished);
};

// Computed property to return sorted tasks
const finishedTaskToFinal = computed(() => {
  return state.tasks.slice().sort((a, b) => a.finished - b.finished);
});

// Updated getFilteredTasks to use finishedTaskToFinal
const getFilteredTasks = computed(() => {
  switch (state.filter) {
    case 'toDo':
      return finishedTaskToFinal.value.filter(task => !task.finished);
    case 'finished':
      return finishedTaskToFinal.value.filter(task => task.finished);
    default:
      return finishedTaskToFinal.value;
  }
});

const registerTask = () => {
  const newTask = {
    title: state.taskTemp,
    finished: false,
  };
  state.tasks.push(newTask);
  state.taskTemp = '';
};

const editTaskTemp = (event) => {
  state.taskTemp = event.target.value;
};

const allTasksFinished = () => {
  return state.filter === 'toDo' && getTaskToDo().length === 0 && state.tasks.length >= 1;
};

const isTaskListEmpty = () => {
  return state.tasks.length === 0;
};

const removeTask = (task) => {
  const index = state.tasks.indexOf(task);
  if (index > -1) {
    state.tasks.splice(index, 1);
  }
};
</script>

<template>
  <div class="container">
    <TaskHeader :tasks-to-do="getTaskToDo().length" />
    <Form :task-temp="state.taskTemp" :edit-task-temp="editTaskTemp" :register-task="registerTask"
      :change-filter="changeFilter" />
    <TaskList :get-filtered-tasks="getFilteredTasks" :all-tasks-finished="allTasksFinished()" :is-task-list-empty="isTaskListEmpty()" :remove-task="removeTask" />
  </div>
</template>

