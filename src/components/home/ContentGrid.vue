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
                        'is-active':
                            activeFilter === filter.value
                    }"
                    :aria-pressed="
                        activeFilter === filter.value
                    "
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
                @play="openVideo"
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


        <!-- =================================================
             VIDEO MODAL
        ================================================== -->

        <VideoModal
            v-if="selectedContent"
            :is-open="true"
            :video-src="selectedContent.video"
            :poster="selectedContent.image"
            :title="selectedContent.title"
            :category="selectedContent.category"
            :description="selectedContent.description"
            :type="selectedContent.type"
            :duration="selectedContent.duration"
            @close="closeVideo"
        />

    </section>
</template>


<script setup>

import {
    computed,
    ref
} from 'vue'

import ContentCard from './ContentCard.vue'

import VideoModal from '../media/VideoModal.vue'


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
// VIDEO ACTIVO
// =============================================================

const selectedContent = ref(null)


// =============================================================
// CONTENIDO
// =============================================================

const contents = [

    {
        id: 1,

        number: '01',

        category: 'Flamenco',

        categoryValue: 'flamenco',

        title:
            'Una noche de flamenco en Cádiz',

        description:
            'Una noche de música, baile y tradición en el corazón de Cádiz.',

        type: 'Vídeo',

        duration: '05:24',

        image:
            'https://images.unsplash.com/photo-1514525253161-7a46d19cd819?auto=format&fit=crop&w=1400&q=80',

        video:
            'https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4'
    },


    {
        id: 2,

        number: '02',

        category: 'Música',

        categoryValue: 'music',

        title:
            'Guitarra flamenca',

        description:
            'El sonido de la guitarra flamenca y la tradición que continúa pasando de generación en generación.',

        type: 'Sesión',

        duration: '08:16',

        image:
            'https://images.unsplash.com/photo-1525201548942-d8732f6617a0?auto=format&fit=crop&w=1200&q=80',

        video:
            'https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4'
    },


    {
        id: 3,

        number: '03',

        category: 'Cultura',

        categoryValue: 'culture',

        title:
            'Cádiz, sus calles y su gente',

        description:
            'Un recorrido por algunos de los rincones y las historias que hacen única a la ciudad.',

        type: 'Documental',

        duration: '12:40',

        image:
            'https://images.unsplash.com/photo-1555881400-74d7acaacd8b?auto=format&fit=crop&w=1200&q=80',

        video:
            'https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4'
    },


    {
        id: 4,

        number: '04',

        category: 'Flamenco',

        categoryValue: 'flamenco',

        title:
            'Palmas y compás',

        description:
            'El ritmo y el compás como parte esencial de la música y el baile flamenco.',

        type: 'Vídeo',

        duration: '05:12',

        image:
            'https://images.unsplash.com/photo-1547153760-18fc86324498?auto=format&fit=crop&w=1200&q=80',

        video:
            'https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4'
    },


    {
        id: 5,

        number: '05',

        category: 'Cultura',

        categoryValue: 'culture',

        title:
            'Tradiciones de Andalucía',

        description:
            'Costumbres, fiestas y tradiciones que siguen formando parte de la vida andaluza.',

        type: 'Reportaje',

        duration: '06:31',

        image:
            'https://images.unsplash.com/photo-1509391366360-2e959784a276?auto=format&fit=crop&w=1200&q=80',

        video:
            'https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4'
    },


    {
        id: 6,

        number: '06',

        category: 'Música',

        categoryValue: 'music',

        title:
            'Música en las calles de Cádiz',

        description:
            'Artistas, músicos y sonidos que llenan las calles de la ciudad.',

        type: 'Corto',

        duration: '09:05',

        image:
            'https://images.unsplash.com/photo-1524368535928-5b5e00ddc76b?auto=format&fit=crop&w=1200&q=80',

        video:
            'https://interactive-examples.mdn.mozilla.net/media/cc0-videos/flower.mp4'
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
            content.categoryValue ===
            activeFilter.value
    )

})


// =============================================================
// ABRIR VIDEO
// =============================================================

const openVideo = (content) => {

    selectedContent.value = content

}


// =============================================================
// CERRAR VIDEO
// =============================================================

const closeVideo = () => {

    selectedContent.value = null

}

</script>