<template>
  <footer class="footer">

    <Logo />

    <nav class="social-buttons">

      <a
        href=""
        target="_blank"
        rel="noopener noreferrer"
        aria-label="Instagram"
      >
        <Instagram class="icon" />
      </a>

      <a
        href=""
        target="_blank"
        rel="noopener noreferrer"
        aria-label="Facebook"
      >
        <Facebook class="icon" />
      </a>

      <a
        href=""
        target="_blank"
        rel="noopener noreferrer"
        aria-label="YouTube"
      >
        <Youtube class="icon" />
      </a>

      <a
        href=""
        target="_blank"
        rel="noopener noreferrer"
        aria-label="TikTok"
      >
        <FontAwesomeIcon
          :icon="faTiktok"
          class="icon"
        />
      </a>

    </nav>

  </footer>
</template>
<script setup>
import { Facebook, Instagram, Youtube } from 'lucide-vue-next';
import Logo from './Logo.vue';
import { faTiktok } from '@fortawesome/free-brands-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

</script>