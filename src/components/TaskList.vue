<script setup>

const props = defineProps(['getFilteredTasks', 'allTasksFinished', 'isTaskListEmpty', 'removeTask']);

</script>

<template>
     <span v-if="props.isTaskListEmpty" class=" generalBackgroundColor text-white text-center fw-semibold w-50 justify-content-center  d-flex rounded-3 position-absolute start-50 translate-middle mt-4 ">List is empty! Let's try add a new
          task to
          do!</span>

     <ul class=" list-group mt-4">
          <li class="list-group-item d-flex align-items-center task" v-for="task in props.getFilteredTasks">
               <input @change="event => task.finished = event.target.checked" :checked="task.finished" :id="task.title"
                    type="checkbox">
               <label :class="{ done: task.finished }" class="ms-3  text-white " :for="task.title">
                    {{ task.title }}
               </label>
               <button @click="props.removeTask(task)" type="button"
                    class="btn btn-outline-danger btn-sm  position-absolute end-0 me-2">X</button>
          </li>
     </ul>
     <span v-if="props.allTasksFinished" class="text-center fw-semibold w-50 justify-content-center text-white d-flex rounded-3 generalBackgroundColor position-absolute start-50 translate-middle mt-4 ">There aren't any tasks to do!
          Great Job!</span>
</template>

<!-- ADICIONAR NÃO HÁ TAREFAS PENDENTES + BOTÃO REMOVER TAREFA  -->

<style scoped>
     .done {
          text-decoration: line-through;
     }

     .generalBackgroundColor{
          background-color: #1e1e1e;
     }

     .task{

          background-color: #4e4e4e;
          border-color: white;
     }
</style>
