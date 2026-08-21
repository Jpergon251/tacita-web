<template>
    <section class="hero">

        <!-- =================================================
             MEDIA
        ================================================== -->

        <div class="hero__media">

            <img
                class="hero__image"
                src="https://images.unsplash.com/photo-1514525253161-7a46d19cd819?auto=format&fit=crop&w=2400&q=85"
                alt=""
                aria-hidden="true"
            />

            <div class="hero__overlay"></div>

        </div>


        <!-- =================================================
             CONTENIDO
        ================================================== -->

        <div class="hero__content">

            <div class="hero__eyebrow">
                <span></span>

                Música · Flamenco · Cultura
            </div>


            <h1 class="hero__title">
                Tacita
                <em>Studio</em>
            </h1>


            <p class="hero__description">
                Una mirada contemporánea a la música,
                la cultura y el carácter de Andalucía.
            </p>


            <div class="hero__actions">

                <RouterLink
                    to="/"
                    class="hero__button hero__button--primary"
                >
                    Descubrir
                </RouterLink>

                <a
                    href="#latest-content"
                    class="hero__button hero__button--secondary"
                >
                    Ver contenido
                </a>

            </div>

        </div>


        <!-- =================================================
             INFORMACIÓN
        ================================================== -->

        <div class="hero__meta">

            <span>
                Cádiz · Andalucía
            </span>

            <span class="hero__meta-line"></span>

            <span>
                01 / 01
            </span>

        </div>


        <!-- =================================================
             SCROLL
        ================================================== -->

        <a
            href="#latest-content"
            class="hero__scroll"
            aria-label="Desplazarse al contenido"
        >
            <span>Scroll</span>

            <span class="hero__scroll-line"></span>
        </a>

    </section>
</template>