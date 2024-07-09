<script setup>
const props = defineProps(['registerTask', 'taskTemp', 'changeFilter', 'editTaskTemp'])
</script>

<template>
     <form @submit.prevent="props.registerTask">
          <div class="row">
               <div class="col">
                    <input :value="props.taskTemp" @change="props.editTaskTemp" required type="text"
                         placeholder="Insert here your task!" class="form-control">
               </div>
               <div class="col-md-2">
                    <button type="submit" class="btn btn-primary">Register</button>
               </div>
               <div class="col-md-2">
                    <select @change="changeFilter" name="" id="" class="form-control">
                         <option value="all">All Tasks</option>
                         <option value="toDo">Tasks To Do</option>
                         <option value="finished">Finished</option>
                    </select>
               </div>
          </div>
     </form>
</template>