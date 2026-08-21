<template>
    <article
        class="content-card"
        :class="{
            'content-card--featured': index === 0
        }"
    >

        <!-- =================================================
             MEDIA
        ================================================== -->

        <div class="content-card__media">

            <img
                :src="content.image"
                :alt="content.title"
                loading="lazy"
            />

            <div class="content-card__overlay"></div>


            <!-- Número -->

            <span class="content-card__number">
                {{ content.number }}
            </span>


            <!-- Tipo -->

            <span class="content-card__type">
                {{ content.type }}
            </span>


            <!-- Play -->

            <button
                type="button"
                class="content-card__play"
                :aria-label="`Reproducir ${content.title}`"
                @click="handlePlay"
            >
                <Play
                    :size="18"
                    :stroke-width="1.5"
                    fill="currentColor"
                />
            </button>

        </div>


        <!-- =================================================
             CONTENT
        ================================================== -->

        <div class="content-card__content">

            <div class="content-card__meta">

                <span class="content-card__category">
                    {{ content.category }}
                </span>

                <span class="content-card__separator"></span>

                <span class="content-card__duration">
                    {{ content.duration }}
                </span>

            </div>


            <h3 class="content-card__title">
                {{ content.title }}
            </h3>


            <p class="content-card__description">
                {{ content.description }}
            </p>


            <button
                type="button"
                class="content-card__link"
                @click="handlePlay"
            >
                <span>Ver contenido</span>

                <ArrowUpRight
                    :size="17"
                    :stroke-width="1.5"
                />
            </button>

        </div>

    </article>
</template>


<script setup>

import {
    ArrowUpRight,
    Play
} from 'lucide-vue-next'


// =============================================================
// PROPS
// =============================================================

const props = defineProps({

    content: {
        type: Object,
        required: true
    },

    index: {
        type: Number,
        default: 0
    }

})


// =============================================================
// EVENTS
// =============================================================

const emit = defineEmits([
    'play'
])


// =============================================================
// PLAY
// =============================================================

const handlePlay = () => {

    emit(
        'play',
        props.content
    )

}

</script>