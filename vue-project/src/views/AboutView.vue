<template>
  <div class="about">
    <TodoList />
  </div>
</template>
<script setup>
import TodoList from '@/components/TodoList.vue'
</script>
<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    /* display: flex;
    align-items: center; */
  }
}
</style>
