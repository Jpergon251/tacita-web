<template>
    <div class="app">
        <Header />

        <main class="main">
            <RouterView />
        </main>

        <Footer />
    </div>
</template>

<script setup>
import Header from './components/layout/Header.vue'
import Footer from './components/layout/Footer.vue'
</script>