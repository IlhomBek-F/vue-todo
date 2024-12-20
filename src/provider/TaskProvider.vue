<script setup>
import { provide, ref } from 'vue';
  const tasks = ref([]);
  const editTaskValue = ref();
  const completedTasks = ref([])
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

  const completeTask = (id) => {
    const foundTask = tasks.value.find((t) => t.id === id);
    tasks.value = tasks.value.filter((t) => t.id !== id);
    completedTasks.value.push({...foundTask, completed: true});
  }

  const unComplete = (status, id) => {
     if(!status) {
       const foundTask = completedTasks.value.find((t) => t.id === id);
       completedTasks.value = completedTasks.value.filter((t) => t.id !== id);
       tasks.value = [...tasks.value, {...foundTask, completed: false}];
     }
  }

  provide('task', {
    completeTask,
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
