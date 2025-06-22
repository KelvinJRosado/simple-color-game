<script setup lang="ts">
import Card from "./Card.vue";
import LanguageToggle from "./LanguageToggle.vue";
import { ref, provide } from "vue";

const language = ref<'en' | 'es'>('en');
provide('language', language);
</script>

<template>
  <LanguageToggle v-model:language="language" />
  <Card
    frontHeader="Color"
    frontText="red"
    backHeader="Color Name"
    backText="Red"
  />
</template>
