<script setup>
import InputText from 'primevue/inputtext';
import { Button } from 'primevue';
import { Menu } from 'primevue';
import { ref , inject} from "vue";
import { FILTER_BY } from '@/core';

const {handleFilter, searchBy} = inject('task');

const menu = ref();
const items = ref([
    {
        label: 'Filter by',
        items: [
            {
              label: 'All',
              icon: 'pi pi-equals',
              command: () => handleFilter(FILTER_BY.ALL)
            },
            {
              label: 'completed',
              icon: 'pi pi-check-circle',
              command: () => handleFilter(FILTER_BY.COMPLETED)
            },
            {
                label: 'not completed',
                icon: 'pi pi-times-circle',
                command: () => handleFilter(FILTER_BY.UNCOMPLETED)
            },
        ]
    }
]);

const toggle = (event) => {
    menu.value.toggle(event);
};
</script>

<template>
   <div class="header">
         Add todo
         <div style="display: flex; gap: 10px;">
           <Button severity="contrast" type="button" icon="pi pi-sliders-v" @click="toggle" aria-haspopup="true" aria-controls="overlay_menu" />
           <Menu ref="menu" id="overlay_menu" :model="items" :popup="true" />
           <InputText type="text" placeholder="search..." v-model="searchBy" />
         </div>
  </div>
</template>

<style>
.header {
  display: flex;
  justify-content: space-between;
}
</style>
