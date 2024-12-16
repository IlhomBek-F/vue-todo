<script setup>
   import Button from 'primevue/button';
   import InputText from 'primevue/inputtext';
   import {ref, defineEmits, watch } from 'vue'

   const newTask = ref('')

   const {editTaskText} = defineProps(['editTaskText'])
   const emit = defineEmits(['handleAddNewTodo']);
    const addNewTodo = () => {
      emit('handleAddNewTodo', {name: newTask.value, completed: false}); // Emit with parameter
      newTask.value = ''
    };

    watch(() => editTaskText, () => {
      newTask.value = editTaskText
    })
</script>

<template>
   <div class="container">
     <InputText class="input" v-model="newTask"/>
     <Button :label="editTaskText ? 'Edit' : 'Add'" @click="addNewTodo" severity="success" />
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
