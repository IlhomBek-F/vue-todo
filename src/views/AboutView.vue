<script setup>
   import Todo from '../components/Todo.vue'
   import Card from 'primevue/card';
   import DataTable from 'primevue/datatable';
   import Column from 'primevue/column';
   import Button from 'primevue/button';
   import {ref} from 'vue';
   const todos = ref([{name: 'Coding'}])
   const editTaskText = ref('')
   const handleAddTodo = (value) => {
        if(editTaskText.value.length) {
          todos.value = todos.value.map((todo) => todo.name === editTaskText.value ? value : todo);
          editTaskText.value = ''
        }else if(value.name.length) {
          todos.value = [...todos.value, value];
        }
   }

   const deleteTask = (t) => {
    todos.value = todos.value.filter((task) => task.name !== t.name);
   };

   const handleEdit = (task) => {
     editTaskText.value = task.name
   };
</script>

<template>
  <Card>
    <template #title>Add todo</template>
    <template #content>
      <Todo @handleAddNewTodo="handleAddTodo" :editTaskText="editTaskText"/>
      <DataTable :value="todos" showGridlines tableStyle="min-width: 50rem">
        <Column field="name" header="Name"></Column>
        <Column header="Action" style="width: 100px; text-align: center;">
          <template #body="{ data }">
             <div class="action">
               <Button icon="pi pi-times" @click="deleteTask(data)" severity="danger" rounded></Button>
               <Button icon="pi pi-pencil" @click="handleEdit(data)" severity="success" rounded></Button>
             </div>
          </template>
        </Column>
      </DataTable>
    </template>
  </Card>
</template>

<style>
 .action {
  display: flex;
  gap: 5px;
 }
</style>

