<template>
  <div class="app">
    <div class="smiley" @click="click">{{ smiley }}</div>
    <div class="points">{{ points }}</div>

    <label>
      Poeng per klikk:
      <input type="number" v-model.number="pointsPerClick" min="1" />
    </label>

    <br />
    <button @click="upgrade" :disabled="!canUpgrade">
      Kjøp oppgradering (10 poeng)
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// --- MODEL ---
const points = ref(0)
const pointsPerClick = ref(1)
const smileyIndex = ref(0)

// --- VIEWMODEL ---
const smiley = computed(() => (smileyIndex.value === 0 ? '😀' : '😁'))
const canUpgrade = computed(() => points.value >= 10)

function click() {
  points.value += pointsPerClick.value
  smileyIndex.value = 1 - smileyIndex.value
}

function upgrade() {
  if (canUpgrade.value) {
    points.value -= 10
    pointsPerClick.value++
  }
}
</script>

<style scoped>
.app {
  font-size: 200%;
  user-select: none;
  text-align: center;
  margin-top: 2rem;
}
.smiley {
  font-size: 300%;
  cursor: pointer;
}
.points {
  margin: 1rem 0;
}
</style>
