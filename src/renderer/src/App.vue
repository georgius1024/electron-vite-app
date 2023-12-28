<script setup>
import { ref } from 'vue'

const dir = ref([])

const scanDir = () => {
  window.electron.ipcRenderer
    .invoke('dir', '.')
    .then((files) => (dir.value = files))
    .catch(console.error)
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
