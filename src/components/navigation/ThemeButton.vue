<template>
    <button
        type="button"
        class="theme-button"
        :aria-label="isDark ? 'Cambiar a modo claro' : 'Cambiar a modo oscuro'"
        :title="isDark ? 'Modo claro' : 'Modo oscuro'"
        @click="toggleTheme"
    >
        <Sun
            v-if="isDark"
            class="theme-button__icon"
            :size="18"
            :stroke-width="1.8"
        />

        <Moon
            v-else
            class="theme-button__icon"
            :size="18"
            :stroke-width="1.8"
        />
    </button>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Sun, Moon } from 'lucide-vue-next'

const isDark = ref(false)

const applyTheme = (dark) => {
    isDark.value = dark

    document.documentElement.dataset.theme = dark
        ? 'dark'
        : 'light'
}

const toggleTheme = () => {
    applyTheme(!isDark.value)

    localStorage.setItem(
        'tacita-theme',
        isDark.value ? 'dark' : 'light'
    )
}

onMounted(() => {
    const savedTheme = localStorage.getItem('tacita-theme')

    if (savedTheme) {
        applyTheme(savedTheme === 'dark')
        return
    }

    const prefersDark = window.matchMedia(
        '(prefers-color-scheme: dark)'
    ).matches

    applyTheme(prefersDark)
})
</script>