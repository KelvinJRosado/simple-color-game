<template>
  <div class="card">
    <h2 class="card-header">Card Header</h2>
    <p class="card-body">This is some placeholder text inside the card.</p>
  </div>
</template>

<script setup lang="ts">
// No props or logic needed for now
</script>

<style scoped>
.card {
  max-width: 350px;
  margin: 2rem auto;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  background: #fff;
}
.card-header {
  text-align: center;
  margin-bottom: 1rem;
  font-size: 1.5rem;
  font-weight: 600;
}
.card-body {
  text-align: center;
  color: #555;
}
</style>
