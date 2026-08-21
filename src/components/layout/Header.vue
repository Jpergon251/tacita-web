<template>
    <header
        class="header"
        :class="{ 'header--scrolled': isScrolled }"
    >

        <div class="header__inner">

            <!-- =================================================
                 LOGO
            ================================================== -->

            <Logo />


            <!-- =================================================
                 DESKTOP NAVIGATION
            ================================================== -->

            <nav
                class="header__nav"
                aria-label="Navegación principal"
            >

                <RouterLink
                    to="/"
                    class="header__link"
                >
                    Inicio
                </RouterLink>

                <!--
                <RouterLink
                    to="/videos"
                    class="header__link"
                >
                    Contenido
                </RouterLink>

                <RouterLink
                    to="/artists"
                    class="header__link"
                >
                    Artistas
                </RouterLink>

                <RouterLink
                    to="/about"
                    class="header__link"
                >
                    Nosotros
                </RouterLink>

                <RouterLink
                    to="/shop"
                    class="header__link"
                >
                    Tienda
                </RouterLink>
                -->

            </nav>


            <!-- =================================================
                 ACTIONS
            ================================================== -->

            <div class="header__actions">

                <ThemeButton />

                <button
                    type="button"
                    class="header__menu-button"
                    :class="{
                        'is-active': isMenuOpen
                    }"
                    :aria-expanded="isMenuOpen"
                    aria-controls="mobile-navigation"
                    aria-label="Abrir menú"
                    @click="toggleMenu"
                >

                    <Menu
                        v-if="!isMenuOpen"
                        :size="20"
                        :stroke-width="1.5"
                    />

                    <X
                        v-else
                        :size="20"
                        :stroke-width="1.5"
                    />

                </button>

            </div>

        </div>


        <!-- =====================================================
             MOBILE NAVIGATION
        ====================================================== -->

        <Transition name="mobile-menu">

            <nav
                v-if="isMenuOpen"
                id="mobile-navigation"
                class="header__mobile-nav"
                aria-label="Navegación móvil"
            >

                <RouterLink
                    to="/"
                    class="header__mobile-link"
                    @click="closeMenu"
                >
                    <span>01</span>
                    Inicio
                </RouterLink>


                <!-- Futuras páginas -->

                <!--
                <RouterLink
                    to="/videos"
                    class="header__mobile-link"
                    @click="closeMenu"
                >
                    <span>02</span>
                    Contenido
                </RouterLink>

                <RouterLink
                    to="/artists"
                    class="header__mobile-link"
                    @click="closeMenu"
                >
                    <span>03</span>
                    Artistas
                </RouterLink>

                <RouterLink
                    to="/about"
                    class="header__mobile-link"
                    @click="closeMenu"
                >
                    <span>04</span>
                    Nosotros
                </RouterLink>

                <RouterLink
                    to="/shop"
                    class="header__mobile-link"
                    @click="closeMenu"
                >
                    <span>05</span>
                    Tienda
                </RouterLink>
                -->

            </nav>

        </Transition>

    </header>
</template>


<script setup>
import {
    onMounted,
    onUnmounted,
    ref,
    watch
} from 'vue'

import {
    Menu,
    X
} from 'lucide-vue-next'

import Logo from './Logo.vue'
import ThemeButton from '../navigation/ThemeButton.vue'


const isMenuOpen = ref(false)
const isScrolled = ref(false)


const handleScroll = () => {
    isScrolled.value = window.scrollY > 40
}


const toggleMenu = () => {
    isMenuOpen.value = !isMenuOpen.value
}


const closeMenu = () => {
    isMenuOpen.value = false
}


watch(isMenuOpen, (isOpen) => {
    document.body.style.overflow = isOpen
        ? 'hidden'
        : ''
})


onMounted(() => {
    handleScroll()

    window.addEventListener(
        'scroll',
        handleScroll,
        { passive: true }
    )
})


onUnmounted(() => {
    window.removeEventListener(
        'scroll',
        handleScroll
    )

    document.body.style.overflow = ''
})
</script>