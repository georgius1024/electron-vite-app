<script setup>
import { ref } from 'vue'
const readDir = window.api.readDir

const dir = ref([])

const scanDir = () => {
  dir.value = readDir('.')
}
</script>

<template>
  <main class="container">
    <button @click="scanDir">Scan dir</button>
    <ul>
      <li v-for="file in dir" :key="file">
        {{ file }}
      </li>
    </ul>
  </main>
</template>
