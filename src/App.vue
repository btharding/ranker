<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <main>
    <div class="sidebar"></div>
    <RouterView />
  </main>
</template>

<style scoped>
  main {
    width: 100vw;
    min-height: 100vh;
    display: flex;
    justify-content: center;
  }
  .sidebar {
    width: 400px;
    height: 100vh;
    }
</style>