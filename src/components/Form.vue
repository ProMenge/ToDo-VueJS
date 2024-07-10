<script setup>
const props = defineProps(['registerTask', 'taskTemp', 'changeFilter', 'editTaskTemp'])
</script>

<template>
     <form @submit.prevent="props.registerTask">
          <div class="row">
               <div class="col">
                    <input :value="props.taskTemp" @change="props.editTaskTemp" required type="text"
                         placeholder="Insert here your task!" class="form-control formBackgroundColor text-white">
               </div>
               <div class="col-md-2">
                    <button type="submit" class="btn buttonPrimary text-black fw-bold">Register</button>
               </div>
               <div class="col-md-2">
                    <select @change="changeFilter" name="" id="" class="form-control text-black fw-bold">
                         <option value="all">All Tasks</option>
                         <option value="toDo">Tasks To Do</option>
                         <option value="finished">Finished</option>
                    </select>
               </div>
          </div>
     </form>
</template>

<style scoped>

     .formBackgroundColor, input:focus{
          background-color: #1e1e1e;
          border-color: #858585
     }

     input::placeholder{
          color: #858585;
     }

     .buttonPrimary{
          background-color: #2e6129;
     }
</style>