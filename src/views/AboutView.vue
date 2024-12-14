<script setup>
   import Todo from '../components/Todo.vue'
   import Card from 'primevue/card';
   import DataTable from 'primevue/datatable';
   import Column from 'primevue/column';
   import Button from 'primevue/button';
   import InputText from 'primevue/inputtext';

   import {ref, watch, computed} from 'vue';
   const todos = ref([{name: 'Coding'}]);
   const editTaskText = ref('');
   const searchValue = ref('');

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

   const filter = computed(() => {
    return todos.value.filter(todo => todo.name.includes(searchValue.value));
   })

</script>

<template>
  <Card>
    <template #title>
       <div class="header">
         Add todo
         <InputText type="text" placeholder="search..." v-model="searchValue" />
       </div>
    </template>
    <template #content>
      <Todo @handleAddNewTodo="handleAddTodo" :editTaskText="editTaskText"/>
      <DataTable :value="filter" showGridlines tableStyle="min-width: 50rem">
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

.header {
  display: flex;
  justify-content: space-between;
}

 .action {
  display: flex;
  gap: 5px;
 }
</style>

