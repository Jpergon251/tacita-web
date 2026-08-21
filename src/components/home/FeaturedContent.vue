<template>
    <section
        id="featured-content"
        class="featured-content"
        aria-labelledby="featured-content-title"
    >

        <!-- =================================================
             HEADER
        ================================================== -->

        <div class="featured-content__header">

            <span class="featured-content__eyebrow">
                01 / Destacado
            </span>

            <span class="featured-content__line"></span>

            <span class="featured-content__category">
                Música
            </span>

        </div>


        <!-- =================================================
             CONTENT
        ================================================== -->

        <article class="featured-content__article">

            <!-- MEDIA -->

            <div class="featured-content__media">

                <img
                    src="https://images.unsplash.com/photo-1501386761578-eac5c94b800a?auto=format&fit=crop&w=1800&q=85"
                    alt="Actuación musical en un escenario"
                    loading="lazy"
                />

                <div class="featured-content__media-overlay"></div>

                <span class="featured-content__duration">
                    04:23
                </span>

            </div>


            <!-- INFORMATION -->

            <div class="featured-content__info">

                <div class="featured-content__number">
                    01
                </div>


                <h2
                    id="featured-content-title"
                    class="featured-content__title"
                >
                    El eco
                    <em>del quejío</em>
                </h2>


                <p class="featured-content__description">
                    Una exploración visual y sonora del flamenco
                    contemporáneo. La tradición, observada desde
                    una nueva perspectiva.
                </p>


                <div class="featured-content__meta">

                    <span>
                        Flamenco
                    </span>

                    <span class="featured-content__meta-dot"></span>

                    <span>
                        Cádiz
                    </span>

                    <span class="featured-content__meta-dot"></span>

                    <span>
                        2026
                    </span>

                </div>


                <RouterLink
                    to="/"
                    class="featured-content__button"
                >
                    <span>
                        Ver contenido
                    </span>

                    <span
                        class="featured-content__button-arrow"
                        aria-hidden="true"
                    >
                        →
                    </span>
                </RouterLink>

            </div>

        </article>


        <!-- =================================================
             FOOTER
        ================================================== -->

        <div class="featured-content__footer">

            <span>
                Tacita Studio
            </span>

            <span class="featured-content__footer-line"></span>

            <span>
                Cultura · Música · Andalucía
            </span>

        </div>

    </section>
</template>