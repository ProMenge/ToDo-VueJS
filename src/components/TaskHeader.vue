<script setup>
const props = defineProps(['tasksToDo'])
</script>

<template>

     <header class="p-5 mb-4 mt-4 bg-light rounded-3">
          <h1>
               My Tasks
          </h1>
          <p>
               You have {{ props.tasksToDo }} tasks to do
          </p>
     </header>

</template>