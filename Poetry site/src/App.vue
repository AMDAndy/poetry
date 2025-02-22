<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <div class="wrapper">
    <header>
      <h1>Poetry</h1>
      <h3>A kind place for words</h3>
    </header>
  </div>

  <RouterView />
</template>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
}

header {
  flex-direction: column;
  text-align: center;
}
</style>
