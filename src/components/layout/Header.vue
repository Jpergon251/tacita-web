<template>
    <header class="header">

        <!-- =====================================================
             BOTÓN MOBILE
        ====================================================== -->

        <button
            type="button"
            class="menu-toggle"
            @click="isMenuOpen = !isMenuOpen"
            :aria-expanded="isMenuOpen"
            :aria-label="
                isMenuOpen
                    ? 'Cerrar menú'
                    : 'Abrir menú'
            "
        >
            <Menu v-if="!isMenuOpen" />
            <X v-else />
        </button>


        <!-- =====================================================
             NAVBAR
        ====================================================== -->

        <nav
            class="navbar"
            :class="{ active: isMenuOpen }"
        >

            <button
                type="button"
                class="menu-toggle"
                @click="isMenuOpen = false"
                aria-label="Cerrar menú"
            >
                <X />
            </button>


            <router-link
                to="/"
                @click="isMenuOpen = false"
            >
                Inicio
            </router-link>


            <!-- =================================================
                 PÁGINAS FUTURAS
            ================================================== -->

            <!--
            <router-link
                to="/videos"
                @click="isMenuOpen = false"
            >
                Videos
            </router-link>

            <router-link
                to="/collections"
                @click="isMenuOpen = false"
            >
                Colecciones
            </router-link>

            <router-link
                to="/shop"
                @click="isMenuOpen = false"
            >
                Tienda
            </router-link>
            -->

        </nav>


        <!-- =====================================================
             LOGO
        ====================================================== -->

        <Logo />


        <!-- =====================================================
             ACTIONS
        ====================================================== -->

        <section class="actions">

            <!-- BUSCADOR -->

            <input
                type="search"
                placeholder="Buscar..."
                aria-label="Buscar"
            />


            <!-- FAVORITOS -->

            <button
                type="button"
                aria-label="Favoritos"
            >
                <Bookmark />
            </button>


            <!-- CARRITO -->

            <button
                type="button"
                aria-label="Carrito"
            >
                <ShoppingBagIcon />
            </button>


            <!-- CAMBIO DE TEMA -->

            <ThemeButton />

        </section>

    </header>
</template>


<script setup>
import { ref, watch } from 'vue'

import {
    Bookmark,
    ShoppingBagIcon,
    Menu,
    X
} from 'lucide-vue-next'

import Logo from './Logo.vue'
import ThemeButton from '../theme/ThemeButton.vue'


// =============================================================
// MOBILE MENU
// =============================================================

const isMenuOpen = ref(false)


// Bloqueamos el scroll del body mientras el menú móvil está abierto.

watch(isMenuOpen, (isOpen) => {
    document.body.style.overflow = isOpen
        ? 'hidden'
        : ''
})
</script>