<template>
    <div class="header">
        <nav class="navbar">

            <router-link to="/"> Inicio </router-link>
            <router-link to="/videos"> Videos </router-link>
            <router-link to="colections"> Colecciones </router-link>
            <router-link to="Shop"> Tienda </router-link>

        </nav>
        <Logo/>
        <section class="actions">
            <input type="search" >
            <button>
                <Bookmark/>
            </button>
            <button>
                <ShoppingBagIcon/> 
                <!-- <ShoppingBasket></ShoppingBasket> -->
            </button>
        </section>
    </div>
</template>

<script setup>
import { Bookmark, ShoppingBag, ShoppingBagIcon, ShoppingBasket } from 'lucide-vue-next';
import Logo from './Logo.vue';


</script>