<template>
  <button
    type="button"
    class="theme-toggle"
    :aria-label="isDark ? 'Cambiar a modo claro' : 'Cambiar a modo oscuro'"
    :title="isDark ? 'Modo claro' : 'Modo oscuro'"
    @click="toggleTheme"
  >
    <Sun
      v-if="isDark"
      class="icon"
    />

    <Moon
      v-else
      class="icon"
    />
  </button>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Sun, Moon } from 'lucide-vue-next'

const isDark = ref(true)

const applyTheme = (theme) => {
  document.documentElement.setAttribute(
    'data-theme',
    theme
  )

  isDark.value = theme === 'dark'
}

const getInitialTheme = () => {
  const savedTheme = localStorage.getItem('tacita-theme')

  if (savedTheme === 'light' || savedTheme === 'dark') {
    return savedTheme
  }

  return window.matchMedia(
    '(prefers-color-scheme: dark)'
  ).matches
    ? 'dark'
    : 'light'
}

const toggleTheme = () => {
  const newTheme = isDark.value
    ? 'light'
    : 'dark'

  applyTheme(newTheme)

  localStorage.setItem(
    'tacita-theme',
    newTheme
  )
}

onMounted(() => {
  applyTheme(getInitialTheme())
})
</script>