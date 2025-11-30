<script setup>
import { ref } from 'vue'
import ShowDate from './components/ShowDate.vue'
import SnowEffect from './components/SnowEffect.vue'
import Slider from './components/Slider.vue'

const showSlider = ref(false)

function handleVacationStarted() {
  showSlider.value = true
}
</script>

<template>
  <SnowEffect />
  <main>
    <ShowDate v-if="!showSlider" @vacation-started="handleVacationStarted" />
    <Slider v-else />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
