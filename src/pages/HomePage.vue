<template>
    <main class="homepage">

        <Hero />

        <FeaturedContent />

        <ContentGrid />

    </main>
</template>

<script setup>
import Hero from '../components/home/Hero.vue'

import FeaturedContent from '../components/home/FeaturedContent.vue'
import ContentGrid from '../components/home/ContentGrid.vue'
</script>