<script setup lang="ts">
import Card from "./Card.vue";
import LanguageToggle from "./LanguageToggle.vue";
import { ref, provide } from "vue";

const language = ref<"en" | "es">("en");
provide("language", language);

const animating = ref(false);
const pendingLanguage = ref<"en" | "es">(language.value);

function handleLanguageChange(val: "en" | "es") {
  if (val === language.value) return;
  animating.value = true;
  pendingLanguage.value = val;
  setTimeout(() => {
    language.value = pendingLanguage.value;
    animating.value = false;
  }, 500); // duration matches CSS
}
</script>

<template>
  <div>
    <LanguageToggle
      :language="pendingLanguage"
      @update:language="handleLanguageChange"
    />
    <Transition name="fade-scale" mode="out-in">
      <Card
        :key="language"
        :frontHeader="{ en: 'Color', es: 'Color' }"
        :frontText="{ en: 'red', es: 'rojo' }"
        :backHeader="{ en: 'Color Name', es: 'Nombre del color' }"
        :backText="{ en: 'Red', es: 'Rojo' }"
      />
    </Transition>
  </div>
</template>

<style scoped>
.fade-scale-enter-active,
.fade-scale-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}
.fade-scale-enter-from,
.fade-scale-leave-to {
  opacity: 0;
  transform: scale(0.97) rotateZ(-2deg);
}
</style>
