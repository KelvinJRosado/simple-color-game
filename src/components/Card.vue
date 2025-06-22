<template>
  <div class="card-container" :class="{ flipped }" @click="flipCard">
    <div class="card">
      <div class="card-face card-front">
        <div
          class="color-visual"
          :style="{ backgroundColor: frontText[currentLang] }"
        ></div>
      </div>
      <div class="card-face card-back">
        <h2 class="card-header">{{ backText[currentLang] }}</h2>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, inject, computed } from "vue";
const language = inject("language", ref<"en" | "es">("en"));

type LangText = { en: string; es: string };

defineProps<{
  frontHeader: LangText;
  frontText: LangText;
  backHeader: LangText;
  backText: LangText;
}>();

const flipped = ref(false);
function flipCard() {
  flipped.value = !flipped.value;
}

const currentLang = computed(() => language?.value || "en");
</script>

<style scoped>
.card-container {
  perspective: 1000px;
  width: 350px;
  margin: 2rem auto;
  cursor: pointer;
}
.card {
  width: 100%;
  height: 220px;
  position: relative;
  transition: transform 0.6s cubic-bezier(0.4, 0.2, 0.2, 1);
  transform-style: preserve-3d;
}
.card-container.flipped .card {
  transform: rotateY(180deg);
}
.card-face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  background: #fff;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.card-front {
  z-index: 2;
}
.card-back {
  transform: rotateY(180deg);
  z-index: 1;
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
.color-visual {
  width: 100px;
  height: 100px;
  border-radius: 0; /* Changed from 50% to 0 for square */
  margin: 0 auto;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.12);
  border: 2px solid #eee;
}
</style>
