<script setup>
const props = defineProps(['tasksToDo'])
</script>

<template>

     <header class="p-5 mb-4 mt-4 headerBackgroundColor text-white rounded-3">
          <h1>
               My Tasks
          </h1>
          <p>
               You have {{ props.tasksToDo }} tasks to do
          </p>
     </header>

</template>

<style scoped>
     .headerBackgroundColor{
          background-color: #1e1e1e;
     }


</style>