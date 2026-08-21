<template>
    <section
        id="latest-content"
        class="content-grid"
        aria-labelledby="content-grid-title"
    >

        <!-- =================================================
             HEADER
        ================================================== -->

        <header class="content-grid__header">

            <div class="content-grid__heading">

                <span class="content-grid__eyebrow">
                    02 / Contenido
                </span>

                <h2
                    id="content-grid-title"
                    class="content-grid__title"
                >
                    Último contenido
                </h2>

            </div>


            <!-- =================================================
                 FILTROS
            ================================================== -->

            <div
                class="content-grid__filters"
                role="group"
                aria-label="Filtrar contenido"
            >

                <button
                    v-for="filter in filters"
                    :key="filter.value"
                    type="button"
                    class="content-grid__filter"
                    :class="{
                        'is-active': activeFilter === filter.value
                    }"
                    :aria-pressed="activeFilter === filter.value"
                    @click="activeFilter = filter.value"
                >
                    {{ filter.label }}
                </button>

            </div>

        </header>


        <!-- =================================================
             GRID
        ================================================== -->

        <div class="content-grid__list">

            <ContentCard
                v-for="(content, index) in filteredContent"
                :key="content.id"
                :content="content"
                :index="index"
            />

        </div>


        <!-- =================================================
             EMPTY STATE
        ================================================== -->

        <div
            v-if="filteredContent.length === 0"
            class="content-grid__empty"
        >
            <span class="content-grid__empty-number">
                00
            </span>

            <p>
                No hay contenido disponible en esta categoría.
            </p>
        </div>

    </section>
</template>


<script setup>
import {
    computed,
    ref
} from 'vue'

import ContentCard from './ContentCard.vue'


// =============================================================
// FILTROS
// =============================================================

const filters = [
    {
        label: 'Todo',
        value: 'all'
    },
    {
        label: 'Música',
        value: 'music'
    },
    {
        label: 'Flamenco',
        value: 'flamenco'
    },
    {
        label: 'Cultura',
        value: 'culture'
    }
]


const activeFilter = ref('all')


// =============================================================
// CONTENIDO
// =============================================================

const contents = [
    {
        id: 1,
        number: '01',
        category: 'Música',
        categoryValue: 'music',
        title: 'El Eco del Quejío',
        description:
            'Una exploración audiovisual del sonido y la emoción del flamenco contemporáneo.',
        type: 'Vídeo',
        duration: '04:23',
        image:
            'https://images.unsplash.com/photo-1514525253161-7a46d19cd819?auto=format&fit=crop&w=1400&q=80'
    },

    {
        id: 2,
        number: '02',
        category: 'Flamenco',
        categoryValue: 'flamenco',
        title: 'Sesión en Vivo',
        description:
            'Una sesión íntima capturada desde la perspectiva del escenario.',
        type: 'Live Session',
        duration: '08:16',
        image:
            'https://images.unsplash.com/photo-1501386761578-eac5c94b800a?auto=format&fit=crop&w=1200&q=80'
    },

    {
        id: 3,
        number: '03',
        category: 'Cultura',
        categoryValue: 'culture',
        title: 'Raíces de la Tacita',
        description:
            'Historias, lugares y personas que forman parte de Cádiz.',
        type: 'Documental',
        duration: '12:40',
        image:
            'https://images.unsplash.com/photo-1539650116574-75c0c6d73f6e?auto=format&fit=crop&w=1200&q=80'
    },

    {
        id: 4,
        number: '04',
        category: 'Música',
        categoryValue: 'music',
        title: 'Entre Palmas',
        description:
            'Ritmo, improvisación y tradición reunidos en una misma sesión.',
        type: 'Performance',
        duration: '05:12',
        image:
            'https://images.unsplash.com/photo-1524368535928-5b5e00ddc76b?auto=format&fit=crop&w=1200&q=80'
    },

    {
        id: 5,
        number: '05',
        category: 'Flamenco',
        categoryValue: 'flamenco',
        title: 'La Soleá',
        description:
            'Una interpretación desnuda de uno de los palos esenciales del flamenco.',
        type: 'Performance',
        duration: '06:31',
        image:
            'https://images.unsplash.com/photo-1547153760-18fc86324498?auto=format&fit=crop&w=1200&q=80'
    },

    {
        id: 6,
        number: '06',
        category: 'Cultura',
        categoryValue: 'culture',
        title: 'Cádiz Después del Sol',
        description:
            'Una mirada documental a la ciudad cuando cae la noche.',
        type: 'Corto',
        duration: '09:05',
        image:
            'https://images.unsplash.com/photo-1555881400-74d7acaacd8b?auto=format&fit=crop&w=1200&q=80'
    }
]


// =============================================================
// CONTENIDO FILTRADO
// =============================================================

const filteredContent = computed(() => {

    if (activeFilter.value === 'all') {
        return contents
    }

    return contents.filter(
        content =>
            content.categoryValue === activeFilter.value
    )
})
</script>