<template>
  <div class="language-toggle">
    <button
      :class="{ active: language === 'en' }"
      @click="$emit('update:language', 'en')"
    >
      English
    </button>
    <button
      :class="{ active: language === 'es' }"
      @click="$emit('update:language', 'es')"
    >
      Español
    </button>
  </div>
</template>

<script lang="ts" setup>
defineProps<{ language: "en" | "es" }>();
const emit = defineEmits(["update:language"]);
</script>

<style scoped>
.language-toggle {
  display: flex;
  gap: 0.5rem;
}
button {
  padding: 0.25rem 0.75rem;
  border: 1px solid #ccc;
  background: #fff;
  cursor: pointer;
  border-radius: 4px;
}
button.active {
  background: #42b983;
  color: #fff;
  border-color: #42b983;
}
</style>
