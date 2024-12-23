<script setup>
   import Todo from '../components/Todo.vue'
   import Card from 'primevue/card';
   import DataTable from 'primevue/datatable';
   import Column from 'primevue/column';
   import Button from 'primevue/button';
   import Checkbox from 'primevue/checkbox';
   import FilterBar from '@/components/FilterBar.vue';
   import { inject } from 'vue';

   const {tasks, editTask, deleteTask, updateTaskStatus} = inject('task');

</script>

<template>
  <Card>
    <template #title>
       <FilterBar />
    </template>
    <template #content>
      <Todo />
      <DataTable :value="tasks" showGridlines >
        <Column field="name" style="width: 30px; text-align: center;">
          <template #header>
               <i class="pi pi-check-circle"></i>
          </template>
          <template #body="{data}">
            <Checkbox v-model="data.completed" binary @update:modelValue="(event) => updateTaskStatus(event, data.id)" :value="data.completed"  />
          </template>
        </Column>
        <Column field="name" header="Task"></Column>
        <Column header="Action" style="width: 100px; text-align: center;">
          <template #body="{ data }">
             <div class="action">
               <Button icon="pi pi-times" @click="deleteTask(data.id)" severity="danger" rounded></Button>
               <Button icon="pi pi-pencil" @click="editTask(data)" severity="success" rounded></Button>
             </div>
          </template>
        </Column>
        <template #empty> No todos found. </template>
      </DataTable>
    </template>
  </Card>
</template>
<style>
 .action {
  display: flex;
  gap: 5px;
 }

 .pi-check-circle {
  color: rgb(0, 189, 0);
 }
</style>

