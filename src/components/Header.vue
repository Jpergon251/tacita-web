<template>
  <header class="header">

    <!-- MENU MOVIL -->
    <button
      class="menu-toggle"
      @click="isMenuOpen = !isMenuOpen"
    >
      <Menu v-if="!isMenuOpen" />
      <X v-else />
    </button>

    <!-- NAVBAR -->
    <nav
      class="navbar"
      :class="{ active: isMenuOpen }"
    >


      <button class="menu-toggle" @click="isMenuOpen = !isMenuOpen">
        <Menu v-if="!isMenuOpen" />
        <X v-else />
      </button>

      <router-link to="/">
        Inicio
      </router-link>

      <router-link to="/videos">
        Videos
      </router-link>

      <router-link to="/collections">
        Colecciones
      </router-link>

      <router-link to="/shop">
        Tienda
      </router-link>
    </nav>

    <!-- LOGO -->
    <Logo />

    <!-- ACTIONS -->
    <section class="actions">
      <input type="search" />

      <button>
        <Bookmark />
      </button>

      <button>
        <ShoppingBagIcon />
      </button>
    </section>

  </header>

</template>

<script setup>
import { ref , watch} from 'vue'
import {
  Bookmark,
  ShoppingBagIcon,
  Menu,
  X
} from 'lucide-vue-next'

import Logo from './Logo.vue'

const isMenuOpen = ref(false)

watch(isMenuOpen, (val) => {
  document.body.style.overflow = val ? 'hidden' : ''
})
</script>