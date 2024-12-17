<script setup>
import { provide, ref } from 'vue';
  const tasks = ref([]);
  const editTaskValue = ref();

  const addTask = (task, edit) => {
     if(edit) {
       tasks.value = tasks.value.map((t) => t.id === task.id ? task : t)
       editTaskValue.value = {};
     } else {
      tasks.value.push(task)
     }
  }

  const editTask = (task) => {
    editTaskValue.value = task;
  }

  const deleteTask = (taskId) => {
     tasks.value = tasks.value.filter((t) => t.id !== taskId);
  }

  provide('task', {
    editTaskValue,
    deleteTask,
    editTask,
    tasks,
    addTask
  })
</script>

<template>
    <slot></slot>
</template>
