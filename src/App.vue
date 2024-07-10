<script setup>
import { reactive } from 'vue';
import TaskHeader from './components/TaskHeader.vue';
import Form from './components/Form.vue';
import TaskList from './components/TaskList.vue';


const state = reactive({
  filter: "All Tasks",
  taskTemp: '',
  tasks: [

  ]
})

const changeFilter = (event) => { state.filter = event.target.value }

const getTaskToDo = () => {
  return state.tasks.filter(task => !task.finished)
}

const getTaskFinished = () => {
  return state.tasks.filter(task => task.finished)
}

const getFilteredTasks = () => {
  switch (state.filter) {
    case 'toDo':
      return getTaskToDo();
    case 'finished':
      return getTaskFinished();
    default:
      return state.tasks;
  }
}

const registerTask = () => {
  const newTask = {
    title: state.taskTemp,
    finished: false,
  }
  state.tasks.push(newTask)
  state.taskTemp = ''

}

const editTaskTemp = (event) => {

  state.taskTemp = event.target.value
}

const allTasksFinished = () => {
  return state.filter === 'toDo' && getTaskToDo().length === 0 && state.tasks.length >= 1;
}

const isTaskListEmpty = () => {
  return state.tasks.length === 0;
};

const removeTask = (task) => {
  const index = state.tasks.indexOf(task);
  if (index > -1) {
    state.tasks.splice(index, 1);
  }
}

// const verifyCheckedTask = (event) => { task.finished = event.target.checked }

</script>

<template>

  <div class="container">
    <TaskHeader :tasks-to-do="getTaskToDo().length" />
    <Form :task-temp="state.taskTemp" :edit-task-temp="editTaskTemp" :register-task="registerTask"
      :change-filter="changeFilter" />
    <TaskList :get-filtered-tasks="getFilteredTasks()" :all-tasks-finished="allTasksFinished()"
      :is-task-list-empty="isTaskListEmpty()" :remove-task="removeTask" />
  </div>
</template>

