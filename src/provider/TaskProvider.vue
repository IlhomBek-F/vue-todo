<script setup>
import { provide, ref } from 'vue';

  const tasks = ref([]);
  const addTask = (task) => {
    tasks.value.push(task)
  }

  provide('task', {
    tasks,
    addTask
  })
</script>

<template>
    <slot></slot>
</template>
