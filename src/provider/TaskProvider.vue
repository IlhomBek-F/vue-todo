<script setup>
import { FILTER_BY } from '@/core';
import { computed, provide, ref } from 'vue';
  const filterBy = ref(FILTER_BY.ALL);
  const searchBy = ref('');
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

    const filteredData = filterObj[filterBy.value];

    if(searchBy.value.trim().length) {
      return filteredData.filter((task) => task.name.startsWith(searchBy.value))
    }

    return filteredData
  });

  const updateTaskStatus = (status, id) => {
    filterBy.value = FILTER_BY.ALL;
    status ? completeTask(id) : unComplete(id)
  }

  const completeTask = (id) => {
    data.value = data.value.map((task) => task.id === id ? {...task, completed: true} : task);
    tasks.value = data.value
  }

  const handleFilter = (filter) => {
     filterBy.value = filter;
  }

  const unComplete = (status, id) => {
     if(!status) {
      data.value = data.value.map((task) => task.id === id ? {...task, completed: false} : task);
     }
  }

  provide('task', {
    updateTaskStatus,
    handleFilter,
    searchBy,
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
