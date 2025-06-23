<template>
  <div class="grid">
    <slot />
  </div>
</template>

<script setup lang="ts">
// No script logic needed for now
</script>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  width: 100%;
}
</style>
