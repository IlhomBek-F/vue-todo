<script setup>
   import Card from 'primevue/card';
   import DataTable from 'primevue/datatable';
   import Column from 'primevue/column';
   import Checkbox from 'primevue/checkbox';
   import {ref, computed, inject} from 'vue';
   const {completedTasks, unComplete} = inject('task');
   const todos = ref([{name: 'Coding'}]);
   const searchValue = ref('');

   const filter = computed(() => {
    return todos.value.filter(todo => todo.name.includes(searchValue.value));
   })

</script>

<template>
  <Card>
    <template #title>Completed</template>
    <template #content>
      <DataTable :value="completedTasks" showGridlines >
        <Column field="name" style="width: 30px; text-align: center;">
          <template #header>
               <i class="pi pi-check-circle"></i>
          </template>
          <template #body="{data}">
            <Checkbox v-model="data.completed" @update:modelValue="(event) => unComplete(event, data.id)" binary inputId="ingredient1"  :value="data.id" />
          </template>
        </Column>
        <Column field="name" header="Task"></Column>
        <template #empty>No completed tasks found.</template>
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
