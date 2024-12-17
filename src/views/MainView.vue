<script setup>
   import Todo from '../components/Todo.vue'
   import Card from 'primevue/card';
   import DataTable from 'primevue/datatable';
   import Column from 'primevue/column';
   import Button from 'primevue/button';
   import InputText from 'primevue/inputtext';

   import Checkbox from 'primevue/checkbox';

   import {ref, computed, inject, watch} from 'vue';
   import { useRouter } from 'vue-router';

   const {tasks, editTask} = inject('task');
   const router = useRouter();
   const searchValue = ref('');

   const deleteTask = (t) => {
    todos.value = todos.value.filter((task) => task.name !== t.name);
   };


   const filter = computed(() => {
    return tasks.value.filter(todo => todo.name.includes(searchValue.value));
   });

   const goToCompletedPage = () => {
    router.push('/completed')
   }

   const onCompleteChange = (evt, id) => {
    console.log(id)
   }

</script>

<template>
  <Card>
    <template #title>
       <div class="header">
         Add todo
         <div style="display: flex; gap: 10px;">
          <Button type="button" label="Completed" @click="goToCompletedPage" icon="pi pi-check-circle" badge="2" badgeSeverity="contrast" variant="outlined" />
           <InputText type="text" placeholder="search..." v-model="searchValue" />
         </div>
       </div>
    </template>
    <template #content>
      <Todo />
      <DataTable :value="filter" showGridlines >
        <Column field="name" style="width: 30px; text-align: center;">
          <template #header>
               <i class="pi pi-check-circle"></i>
          </template>
          <template #body="{data}">
            <Checkbox :model="data.completed" @value-change="(event) => onCompleteChange(event, data.id)" :value="true"  />
          </template>
        </Column>
        <Column field="name" header="Task"></Column>
        <Column header="Action" style="width: 100px; text-align: center;">
          <template #body="{ data }">
             <div class="action">
               <Button icon="pi pi-times" @click="deleteTask(data)" severity="danger" rounded></Button>
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

.header {
  display: flex;
  justify-content: space-between;
}

 .action {
  display: flex;
  gap: 5px;
 }

 .pi-check-circle {
  color: rgb(0, 189, 0);
 }
</style>

