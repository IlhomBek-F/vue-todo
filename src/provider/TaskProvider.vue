<script setup>
import { provide, ref } from 'vue';
  const tasks = ref([]);
  const editTaskValue = ref();

  const addTask = (task, edit) => {
     if(edit) {
       tasks.value.map((t) => t.id === task.id ? task : t)
     } else {
        tasks.value.push(task)
     }
  }

  const editTask = (task) => {
    editTaskValue.value = task;
  }

  provide('task', {
    editTaskValue,
    editTask,
    tasks,
    addTask
  })
</script>

<template>
    <slot></slot>
</template>
