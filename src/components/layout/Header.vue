<template>
    <header
        class="header"
        :class="{
            'header--scrolled': isScrolled
        }"
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


                <!-- Futuras páginas -->

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

                <SearchButton />

                <ThemeButton />


                <!-- =================================================
                     MOBILE MENU TRIGGER
                ================================================== -->

                <button
                    type="button"
                    class="header__menu-button"
                    :class="{
                        'is-active': isMenuOpen
                    }"
                    :aria-expanded="isMenuOpen"
                    aria-controls="mobile-navigation"
                    :aria-label="
                        isMenuOpen
                            ? 'Cerrar menú'
                            : 'Abrir menú'
                    "
                    @click="toggleMenu"
                >

                    <span
                        class="header__menu-icon"
                        :class="{
                            'is-active': isMenuOpen
                        }"
                    ></span>

                </button>

            </div>

        </div>


        <!-- =====================================================
             MOBILE NAVIGATION
        ====================================================== -->

        <MobileMenu
            :is-open="isMenuOpen"
            @close="closeMenu"
        />

    </header>
</template>


<script setup>
import {
    onMounted,
    onUnmounted,
    ref,
    watch
} from 'vue'


import Logo from './Logo.vue'

import SearchButton from '../navigation/SearchButton.vue'
import ThemeButton from '../navigation/ThemeButton.vue'
import MobileMenu from '../navigation/MobileMenu.vue'


const isMenuOpen = ref(false)

const isScrolled = ref(false)


const handleScroll = () => {

    isScrolled.value =
        window.scrollY > 40
}


const toggleMenu = () => {

    isMenuOpen.value =
        !isMenuOpen.value
}


const closeMenu = () => {

    isMenuOpen.value = false
}


watch(
    isMenuOpen,
    (isOpen) => {

        document.body.style.overflow =
            isOpen
                ? 'hidden'
                : ''
    }
)


onMounted(() => {

    handleScroll()

    window.addEventListener(
        'scroll',
        handleScroll,
        {
            passive: true
        }
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