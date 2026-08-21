<template>
    <footer class="footer">

        <div class="footer__inner">

            <!-- =================================================
                 BRAND
            ================================================== -->

            <div class="footer__brand">

                <Logo />

                <p class="footer__tagline">
                    Música, cultura y carácter
                    desde el sur.
                </p>

            </div>


            <!-- =================================================
                 NAVIGATION
            ================================================== -->

            <nav
                class="footer__navigation"
                aria-label="Navegación del pie de página"
            >

                <span class="footer__label">
                    Navegación
                </span>

                <ul class="footer__links">

                    <li>
                        <RouterLink
                            to="/"
                            class="footer__link"
                        >
                            Inicio
                        </RouterLink>
                    </li>

                    <!-- Futuras páginas -->

                    <!--
                    <li>
                        <RouterLink
                            to="/content"
                            class="footer__link"
                        >
                            Contenido
                        </RouterLink>
                    </li>

                    <li>
                        <RouterLink
                            to="/artists"
                            class="footer__link"
                        >
                            Artistas
                        </RouterLink>
                    </li>

                    <li>
                        <RouterLink
                            to="/about"
                            class="footer__link"
                        >
                            Nosotros
                        </RouterLink>
                    </li>

                    <li>
                        <RouterLink
                            to="/shop"
                            class="footer__link"
                        >
                            Tienda
                        </RouterLink>
                    </li>
                    -->

                </ul>

            </nav>


            <!-- =================================================
                 SOCIAL
            ================================================== -->

            <div class="footer__social">

                <span class="footer__label">
                    Síguenos
                </span>

                <div class="footer__social-links">

                    <a
                        href="#"
                        class="footer__social-link"
                        aria-label="Instagram"
                    >
                        <svg
                            viewBox="0 0 24 24"
                            aria-hidden="true"
                        >
                            <path :d="siInstagram.path" />
                        </svg>

                        <span>Instagram</span>
                    </a>


                    <a
                        href="#"
                        class="footer__social-link"
                        aria-label="YouTube"
                    >
                        <svg
                            viewBox="0 0 24 24"
                            aria-hidden="true"
                        >
                            <path :d="siYoutube.path" />
                        </svg>

                        <span>YouTube</span>
                    </a>


                    <a
                        href="#"
                        class="footer__social-link"
                        aria-label="TikTok"
                    >
                        <svg
                            viewBox="0 0 24 24"
                            aria-hidden="true"
                        >
                            <path :d="siTiktok.path" />
                        </svg>

                        <span>TikTok</span>
                    </a>

                </div>

            </div>

            <!-- =================================================
                 LOCATION
            ================================================== -->

            <div class="footer__location">

                <span class="footer__label">
                    Desde
                </span>

                <p>
                    Cádiz
                    <span>·</span>
                    Andalucía
                </p>

            </div>


            <!-- =================================================
                 BOTTOM
            ================================================== -->

            <div class="footer__bottom">

                <span class="footer__copyright">
                    © {{ currentYear }} Tacita Studio
                </span>

                <span class="footer__edition">
                    Música · Flamenco · Cultura
                </span>

            </div>

        </div>

    </footer>
</template>


<script setup>
import { computed } from 'vue'
import {
    siInstagram,
    siYoutube,
    siTiktok
} from 'simple-icons/icons'

import Logo from './Logo.vue'

const currentYear = computed(() => {
    return new Date().getFullYear()
})
</script>