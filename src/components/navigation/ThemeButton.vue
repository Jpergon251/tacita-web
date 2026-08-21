<template>
    <button
        type="button"
        class="theme-button"
        :aria-label="
            isDark
                ? 'Cambiar a modo claro'
                : 'Cambiar a modo oscuro'
        "
        :aria-pressed="isDark"
        @click="toggleTheme"
    >

        <Transition
            name="theme-icon"
            mode="out-in"
        >

            <Moon
                v-if="isDark"
                key="dark"
                :size="19"
                :stroke-width="1.5"
            />

            <Sun
                v-else
                key="light"
                :size="19"
                :stroke-width="1.5"
            />

        </Transition>

    </button>
</template>


<script setup>
import {
    onMounted,
    ref
} from 'vue'

import {
    Moon,
    Sun
} from 'lucide-vue-next'


const isDark = ref(false)


const applyTheme = (dark) => {

    document.documentElement.dataset.theme =
        dark
            ? 'dark'
            : 'light'
}


const toggleTheme = () => {

    isDark.value = !isDark.value

    applyTheme(isDark.value)

    localStorage.setItem(
        'tacita-theme',
        isDark.value
            ? 'dark'
            : 'light'
    )
}


onMounted(() => {

    const savedTheme =
        localStorage.getItem('tacita-theme')


    if (savedTheme) {

        isDark.value =
            savedTheme === 'dark'

    } else {

        isDark.value =
            window.matchMedia(
                '(prefers-color-scheme: dark)'
            ).matches
    }


    applyTheme(isDark.value)
})
</script>