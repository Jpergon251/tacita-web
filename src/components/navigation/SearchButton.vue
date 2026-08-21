<template>
    <div
        class="search-button"
        :class="{
            'search-button--open': isOpen
        }"
    >

        <!-- =================================================
             BOTÓN
        ================================================== -->

        <button
            type="button"
            class="search-button__trigger"
            :aria-expanded="isOpen"
            aria-label="Buscar"
            @click="toggleSearch"
        >
            <Search
                :size="20"
                :stroke-width="1.5"
            />
        </button>


        <!-- =================================================
             BUSCADOR
        ================================================== -->

        <Transition name="search">

            <form
                v-if="isOpen"
                class="search-button__form"
                @submit.prevent="handleSearch"
            >

                <label
                    for="site-search"
                    class="sr-only"
                >
                    Buscar contenido
                </label>

                <input
                    id="site-search"
                    ref="searchInput"
                    v-model="query"
                    type="search"
                    placeholder="Buscar..."
                    autocomplete="off"
                />


                <button
                    v-if="query"
                    type="button"
                    class="search-button__clear"
                    aria-label="Borrar búsqueda"
                    @click="clearSearch"
                >
                    <X
                        :size="16"
                        :stroke-width="1.5"
                    />
                </button>

            </form>

        </Transition>

    </div>
</template>


<script setup>
import {
    nextTick,
    ref,
    watch
} from 'vue'

import {
    Search,
    X
} from 'lucide-vue-next'


const isOpen = ref(false)

const query = ref('')

const searchInput = ref(null)


const toggleSearch = async () => {

    isOpen.value = !isOpen.value

    if (isOpen.value) {

        await nextTick()

        searchInput.value?.focus()
    }
}


const clearSearch = () => {

    query.value = ''

    searchInput.value?.focus()
}


const closeSearch = () => {

    isOpen.value = false

    query.value = ''
}


const handleSearch = () => {

    const search = query.value.trim()

    if (!search) {
        return
    }

    // La lógica real de búsqueda se conectará
    // cuando tengamos el sistema de contenido.

    console.log('Búsqueda:', search)
}


watch(isOpen, (value) => {

    if (!value) {
        query.value = ''
    }
})


defineExpose({
    closeSearch
})
</script>