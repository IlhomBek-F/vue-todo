<script setup>
   import Card from 'primevue/card';
   import DataTable from 'primevue/datatable';
   import Column from 'primevue/column';
   import Checkbox from 'primevue/checkbox';
   import {ref, computed} from 'vue';
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
      <DataTable :value="filter" showGridlines >
        <Column field="name" style="width: 30px; text-align: center;">
          <template #header>
               <i class="pi pi-check-circle"></i>
          </template>
          <template #body="{data}">
            <Checkbox :model="data.completed" inputId="ingredient1" name="pizza" value="Cheese" />
          </template>
        </Column>
        <Column field="name" header="Task"></Column>
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
