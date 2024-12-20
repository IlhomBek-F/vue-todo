<script setup>
import { FILTER_BY } from '@/core';
import { computed, provide, ref } from 'vue';
  const filterBy = ref(FILTER_BY.ALL);
  const data = ref([]);
  const editTaskValue = ref();
  const completedTasks = ref([]);

  const addTask = (task, edit) => {
     if(edit) {
      data.value = data.value.map((t) => t.id === task.id ? task : t)
       editTaskValue.value = {};
     } else {
      data.value.push(task)
     }
  }

  const editTask = (task) => {
    editTaskValue.value = task;
  }

  const deleteTask = (taskId) => {
    data.value = data.value.filter((t) => t.id !== taskId);
  }

  const tasks = computed(() => {
    const filterObj = {
      [FILTER_BY.ALL]: data.value,
      [FILTER_BY.COMPLETED]: data.value.filter((task) => task.completed),
      [FILTER_BY.UNCOMPLETED]: data.value.filter((task) => !task.completed)
    };

    return filterObj[filterBy.value]
  });

  const completeTask = (id) => {
    const foundTask = tasks.value.find((t) => t.id === id);
    data.value = data.value.filter((t) => t.id !== id);
    completedTasks.value.push({...foundTask, completed: true});
  }

  const handleFilter = (filter) => {
     filterBy.value = filter
  }

  const unComplete = (status, id) => {
     if(!status) {
       const foundTask = completedTasks.value.find((t) => t.id === id);
       completedTasks.value = completedTasks.value.filter((t) => t.id !== id);
       data.value = [...data.value, {...foundTask, completed: false}];
     }
  }

  provide('task', {
    completeTask,
    handleFilter,
    unComplete,
    editTaskValue,
    completedTasks,
    deleteTask,
    editTask,
    tasks,
    addTask
  })
</script>

<template>
    <slot></slot>
</template>
