<script setup lang="ts">
import Card from "./Card.vue";
import LanguageToggle from "./LanguageToggle.vue";
import Grid from "./Grid.vue";
import { ref, provide } from "vue";

const language = ref<"en" | "es">("en");
provide("language", language);

const pendingLanguage = ref<"en" | "es">(language.value);
const showCard = ref(true);
const flipped = ref(false);

function handleLanguageChange(val: "en" | "es") {
  if (val === language.value) return;
  showCard.value = false; // trigger leave
  pendingLanguage.value = val;
}

function onAfterLeave() {
  language.value = pendingLanguage.value;
  showCard.value = true; // trigger enter
}

function handleFlip() {
  flipped.value = !flipped.value;
}
</script>

<template>
  <div>
    <LanguageToggle
      :language="pendingLanguage"
      @update:language="handleLanguageChange"
    />
    <Grid>
      <Transition name="fade-scale" mode="out-in" @after-leave="onAfterLeave">
        <div v-if="showCard" class="card-row">
          <Card
            :flipped="flipped"
            @flip="handleFlip"
            frontHeader="Color"
            frontText="red"
            :backHeader="{ en: 'Color Name', es: 'Nombre del color' }"
            :backText="{ en: 'Red', es: 'Rojo' }"
          />
          <Card
            :flipped="false"
            frontHeader="Color"
            frontText="blue"
            :backHeader="{ en: 'Color Name', es: 'Nombre del color' }"
            :backText="{ en: 'Blue', es: 'Azul' }"
          />
          <Card
            :flipped="false"
            frontHeader="Color"
            frontText="yellow"
            :backHeader="{ en: 'Color Name', es: 'Nombre del color' }"
            :backText="{ en: 'Yellow', es: 'Amarillo' }"
          />
        </div>
      </Transition>
    </Grid>
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
