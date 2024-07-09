<script setup>

import { reactive } from 'vue';

const state = reactive({
  filter: "All Tasks",
  tasks: [
    {
      title: 'Study ES6+',
      finished: false,
    },
    {
      title: 'Study SASS',
      finished: true,
    },
    {
      title: 'Study ReactJS',
      finished: false,
    }
  ]
})

const accessFilter = (event) => { state.filter = event.target.value }

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

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>
        My Tasks
      </h1>
      <p>
        You have {{ getTaskToDo().length }} tasks to do
      </p>
    </header>
    <form action="">
      <div class="row">
        <div class="col">
          <input type="text" placeholder="Insert here your task!" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Register</button>
        </div>
        <div class="col-md-2">
          <select @change="accessFilter" name="" id="" class="form-control">
            <option value="all">All Tasks</option>
            <option value="toDo">Tasks To Do</option>
            <option value="finished">Finished</option>
          </select>
        </div>
      </div>
    </form>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getFilteredTasks()">
        <input :checked="task.finished" :id="task.title" type="checkbox">
        <label :class="{ done: task.finished }" class="ms-3" :for="task.title">
          {{ task.title }}
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
