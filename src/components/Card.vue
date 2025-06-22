<template>
  <div class="card-container" :class="{ flipped }" @click="flipCard">
    <div class="card">
      <div class="card-face card-front">
        <h2 class="card-header">{{ frontHeader }}</h2>
        <p class="card-body">{{ frontText }}</p>
      </div>
      <div class="card-face card-back">
        <h2 class="card-header">{{ backHeader }}</h2>
        <p class="card-body">{{ backText }}</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
const props = defineProps<{
  frontHeader: string;
  frontText: string;
  backHeader: string;
  backText: string;
}>();
const flipped = ref(false);
function flipCard() {
  flipped.value = !flipped.value;
}
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
</style>
