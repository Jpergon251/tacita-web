<template>
    <Transition name="video-modal">

        <div
            v-if="isOpen"
            class="video-modal"
            role="dialog"
            aria-modal="true"
            :aria-labelledby="titleId"
            @mousedown.self="close"
        >

            <!-- =================================================
                 BACKDROP
            ================================================== -->

            <div
                class="video-modal__backdrop"
                aria-hidden="true"
            ></div>


            <!-- =================================================
                 CONTAINER
            ================================================== -->

            <div class="video-modal__container">

                <!-- =================================================
                     HEADER
                ================================================== -->

                <header class="video-modal__header">

                    <div class="video-modal__heading">

                        <span
                            v-if="category"
                            class="video-modal__category"
                        >
                            {{ category }}
                        </span>

                        <h2
                            :id="titleId"
                            class="video-modal__title"
                        >
                            {{ title }}
                        </h2>

                    </div>


                    <!-- =================================================
                         CLOSE
                    ================================================== -->

                    <button
                        type="button"
                        class="video-modal__close"
                        aria-label="Cerrar reproductor"
                        @click="close"
                    >
                        <X
                            :size="22"
                            :stroke-width="1.5"
                        />
                    </button>

                </header>


                <!-- =================================================
                     VIDEO
                ================================================== -->

                <div class="video-modal__player">

                    <video
                        ref="videoElement"
                        class="video-modal__video"
                        :src="videoSrc"
                        :poster="poster"
                        controls
                        playsinline
                        preload="metadata"
                        @loadedmetadata="handleMetadata"
                        @error="handleVideoError"
                    >
                        Tu navegador no soporta la reproducción de vídeo.
                    </video>


                    <!-- =================================================
                         LOADING
                    ================================================== -->

                    <Transition name="video-loading">

                        <div
                            v-if="isLoading"
                            class="video-modal__loading"
                            aria-live="polite"
                        >
                            <span class="video-modal__spinner"></span>

                            <span>
                                Cargando vídeo...
                            </span>
                        </div>

                    </Transition>


                    <!-- =================================================
                         ERROR
                    ================================================== -->

                    <Transition name="video-error">

                        <div
                            v-if="hasError"
                            class="video-modal__error"
                            role="alert"
                        >

                            <div class="video-modal__error-icon">
                                <AlertCircle
                                    :size="28"
                                    :stroke-width="1.5"
                                />
                            </div>

                            <strong>
                                No se puede reproducir este vídeo
                            </strong>

                            <p>
                                El contenido no está disponible
                                actualmente.
                            </p>

                            <button
                                type="button"
                                class="video-modal__retry"
                                @click="retry"
                            >
                                Intentar de nuevo
                            </button>

                        </div>

                    </Transition>

                </div>


                <!-- =================================================
                     FOOTER / INFO
                ================================================== -->

                <footer class="video-modal__footer">

                    <div class="video-modal__meta">

                        <span v-if="type">
                            {{ type }}
                        </span>

                        <span
                            v-if="duration"
                            class="video-modal__meta-separator"
                            aria-hidden="true"
                        >
                            /
                        </span>

                        <span v-if="duration">
                            {{ duration }}
                        </span>

                    </div>


                    <p
                        v-if="description"
                        class="video-modal__description"
                    >
                        {{ description }}
                    </p>

                </footer>

            </div>

        </div>

    </Transition>
</template>


<script setup>
import {
    nextTick,
    onBeforeUnmount,
    ref,
    watch
} from 'vue'

import {
    AlertCircle,
    X
} from 'lucide-vue-next'


// =============================================================
// PROPS
// =============================================================

const props = defineProps({

    isOpen: {
        type: Boolean,
        default: false
    },

    videoSrc: {
        type: String,
        required: true
    },

    poster: {
        type: String,
        default: ''
    },

    title: {
        type: String,
        default: 'Reproducción'
    },

    category: {
        type: String,
        default: ''
    },

    description: {
        type: String,
        default: ''
    },

    type: {
        type: String,
        default: ''
    },

    duration: {
        type: String,
        default: ''
    }
})


// =============================================================
// EMITS
// =============================================================

const emit = defineEmits([
    'close'
])


// =============================================================
// REFS
// =============================================================

const videoElement = ref(null)

const isLoading = ref(false)

const hasError = ref(false)


// =============================================================
// ACCESSIBILITY
// =============================================================

const titleId = `video-modal-title-${Math.random()
    .toString(36)
    .slice(2)}`


// =============================================================
// CLOSE
// =============================================================

const close = () => {

    stopVideo()

    emit('close')
}


// =============================================================
// VIDEO
// =============================================================

const stopVideo = () => {

    if (!videoElement.value) {
        return
    }

    videoElement.value.pause()

    videoElement.value.currentTime = 0
}


const handleMetadata = () => {

    isLoading.value = false

    hasError.value = false
}


const handleVideoError = () => {

    isLoading.value = false

    hasError.value = true
}


const retry = async () => {

    if (!videoElement.value) {
        return
    }

    hasError.value = false

    isLoading.value = true

    videoElement.value.load()

    await nextTick()

    videoElement.value.play()
        .catch(() => {
            // El navegador puede bloquear
            // la reproducción automática.
        })
}


// =============================================================
// KEYBOARD
// =============================================================

const handleKeydown = (event) => {

    if (!props.isOpen) {
        return
    }

    if (event.key === 'Escape') {
        close()
    }
}


// =============================================================
// BODY SCROLL
// =============================================================

const updateBodyScroll = (isOpen) => {

    document.body.style.overflow =
        isOpen
            ? 'hidden'
            : ''
}


// =============================================================
// WATCH
// =============================================================

watch(
    () => props.isOpen,
    async (isOpen) => {

        updateBodyScroll(isOpen)

        if (!isOpen) {

            stopVideo()

            return
        }

        hasError.value = false

        isLoading.value = true

        await nextTick()

        videoElement.value?.focus()
    },
    {
        immediate: true
    }
)


// =============================================================
// LIFECYCLE
// =============================================================

window.addEventListener(
    'keydown',
    handleKeydown
)


onBeforeUnmount(() => {

    window.removeEventListener(
        'keydown',
        handleKeydown
    )

    document.body.style.overflow = ''
})
</script>