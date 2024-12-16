<script setup lang="ts">
import {  RouterView } from 'vue-router'
import TaskProvider from './provider/TaskProvider.vue';
</script>

<template>
   <TaskProvider>
     <RouterView />
   </TaskProvider>
</template>

