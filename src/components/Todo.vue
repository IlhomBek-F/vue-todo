<script setup>
   import Button from 'primevue/button';
   import InputText from 'primevue/inputtext';
   import {ref, defineEmits, watch, inject } from 'vue'

  const newTask = ref('')
  const {addTask, editTaskValue, editTask} = inject('task');

  watch(editTaskValue, (newValue) => {
      newTask.value = newValue.name
  })

   const emit = defineEmits(['handleAddNewTodo']);
    const addNewTodo = () => {
        if(editTaskValue.value?.id) {
          addTask({...editTaskValue, name: newTask.value}, true)
        } else {
          addTask({name: newTask.value, completed: false, id: Math.random() * 1000}, false)
        }
      newTask.value = ''
    };


</script>

<template>
   <div class="container">
     <InputText class="input" v-model="newTask"/>
     <Button :label="editTaskValue ? 'Edit' : 'Add'" @click="addNewTodo" severity="success" />
   </div>
</template>

<style>
  .container {
    margin-bottom: 10px;
    display: flex;
    justify-content: space-between;
    width: 100%;
    gap: 10px;
  }

  .input {
    width: 100%;
  }
</style>
