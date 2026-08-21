<template>
    <Transition name="mobile-menu">

        <nav
            v-if="isOpen"
            id="mobile-navigation"
            class="mobile-menu"
            aria-label="Navegación móvil"
        >

            <!-- ================================================
                 HEADER DEL MENÚ
            ================================================= -->

            <div class="mobile-menu__header">

                <span class="mobile-menu__label">
                    Menú
                </span>

                <button
                    type="button"
                    class="mobile-menu__close"
                    aria-label="Cerrar menú"
                    @click="closeMenu"
                >
                    <X
                        :size="22"
                        :stroke-width="1.5"
                    />
                </button>

            </div>


            <!-- ================================================
                 NAVEGACIÓN
            ================================================= -->

            <ul class="mobile-menu__list">

                <li>
                    <RouterLink
                        to="/"
                        class="mobile-menu__link"
                        @click="closeMenu"
                    >
                        <span class="mobile-menu__number">
                            01
                        </span>

                        <span class="mobile-menu__text">
                            Inicio
                        </span>
                    </RouterLink>
                </li>


                <li>
                    <a
                        href="#latest-content"
                        class="mobile-menu__link"
                        @click="closeMenu"
                    >
                        <span class="mobile-menu__number">
                            02
                        </span>

                        <span class="mobile-menu__text">
                            Contenido
                        </span>
                    </a>
                </li>


                <!-- ============================================
                     FUTURAS PÁGINAS
                ============================================= -->

                <!--

                <li>
                    <RouterLink
                        to="/artists"
                        class="mobile-menu__link"
                        @click="closeMenu"
                    >
                        <span class="mobile-menu__number">
                            03
                        </span>

                        <span class="mobile-menu__text">
                            Artistas
                        </span>
                    </RouterLink>
                </li>

                <li>
                    <RouterLink
                        to="/about"
                        class="mobile-menu__link"
                        @click="closeMenu"
                    >
                        <span class="mobile-menu__number">
                            04
                        </span>

                        <span class="mobile-menu__text">
                            Nosotros
                        </span>
                    </RouterLink>
                </li>

                <li>
                    <RouterLink
                        to="/shop"
                        class="mobile-menu__link"
                        @click="closeMenu"
                    >
                        <span class="mobile-menu__number">
                            05
                        </span>

                        <span class="mobile-menu__text">
                            Tienda
                        </span>
                    </RouterLink>
                </li>

                -->

            </ul>


            <!-- ================================================
                 FOOTER DEL MENÚ
            ================================================= -->

            <div class="mobile-menu__footer">

                <span>
                    Cádiz · Andalucía
                </span>

                <span>
                    Tacita Studio
                </span>

            </div>

        </nav>

    </Transition>
</template>


<script setup>
import { X } from 'lucide-vue-next'


defineProps({
    isOpen: {
        type: Boolean,
        default: false
    }
})


const emit = defineEmits([
    'close'
])


const closeMenu = () => {
    emit('close')
}
</script>