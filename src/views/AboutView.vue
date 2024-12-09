<script setup>
   import Todo from '../components/Todo.vue'
   import Card from 'primevue/card';
   import DataTable from 'primevue/datatable';
   import Column from 'primevue/column';
   import Button from 'primevue/button';

   import {ref} from 'vue';

   const todos = ref([{name: 'Coding'}])

   const handleAddTodo = (value) => {
        if(value.name.length) {
          todos.value = [...todos.value, value];
        }
   }

   const deleteTask = (t) => {
    todos.value = todos.value.filter((task) => task.name !== t.name);
   };

</script>

<template>
  <Card>
    <template #title>Add todo</template>
    <template #content>
      <Todo @handleAddNewTodo="handleAddTodo"/>
      <DataTable :value="todos" showGridlines tableStyle="min-width: 50rem">
        <Column field="name" header="Name"></Column>
        <Column header="Action" style="width: 100px; text-align: center;">
          <template #body="{ data }">
            <Button icon="pi pi-times" @click="deleteTask(data)" severity="secondary" rounded></Button>
          </template>
        </Column>
      </DataTable>
    </template>
  </Card>
</template>

