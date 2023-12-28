<script setup>
import { ref } from 'vue'

const dir = ref([])

window.electron.ipcRenderer.on('files', (event, files) => {
  dir.value = files
})

const scanDir = () => {
  window.electron.ipcRenderer
    .invoke('dir', '.')
    .then((files) => (dir.value = files))
    .catch(console.error)
  window.electron.ipcRenderer.send('watch', '.')
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
