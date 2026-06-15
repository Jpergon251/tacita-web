<template>
    <div class="footer">
        <Logo/>
        <nav class="social-buttons">
            <a href="">
                <Instagram class="icon"/>
            </a>
            <a href="">
                <Facebook class="icon"/>
            </a>
            <a href="">
                <Youtube class="icon"/>
            </a>
            <a href="">
                <FontAwesomeIcon :icon="faTiktok" class="icon"/>
            </a>
        </nav>
    </div>
</template>
<script setup>
import { Facebook, Instagram, Youtube } from 'lucide-vue-next';
import Logo from './Logo.vue';
import { faTiktok } from '@fortawesome/free-brands-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';

</script>