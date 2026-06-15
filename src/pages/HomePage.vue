<template>
  <div class="homepage">
      <section class="start-info">
        <video 
        :src="video_placeholder"
        autoplay
        muted
        loop
        playsinline
        >
        </video>
        <span>Pabloputero</span>
      </section>

      <h2 class="section-title">
        <DiamondPlus class="icon"/>
        Últimos vídeos
      </h2>
      <section class="last-videos-hor">
        <video 
        :src="video_placeholder"
        controls
        >
        </video>
        <article>
          <h2>
            Lorem ipsum dolor sit amet.
          </h2>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Aspernatur voluptas unde voluptates repudiandae ipsa iure dolor quisquam, recusandae eveniet earum velit ipsum. Voluptatibus libero quia temporibus dolorem, similique earum vel.
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Doloribus optio magnam nostrum repellendus obcaecati at, molestiae nesciunt! Porro unde, provident, illum accusantium quo at, sed animi molestiae aspernatur impedit odio?
          </p>
        </article>
      </section>
      <h2 class="section-title">
        <DiamondPlus class="icon"/>
        Shorts
      </h2>
      <section class="last-videos-ver">
        <button class="carousel-btn left" @click="scrollLeft">
          <ArrowBigLeftDash class="icon" fill="currentColor"/>
        </button>

        <ul class="shorts-list" ref="shortsContainer">
          <li
            class="shorts-item"
            v-for="(item, index) in 10"
            :key="index"
          >
            <video
              :src="video_placegolder_vert"
              controls
            />
          </li>
        </ul>

        <button class="carousel-btn right" @click="scrollRight">
          <ArrowBigRightDash class="icon" fill="currentColor"/>
        </button>
      </section>
  </div>

</template>

<script setup>

import { ArrowBigLeftDash, ArrowBigRightDash, DiamondPlus } from 'lucide-vue-next'
import { ref } from 'vue'

const shortsContainer = ref(null)

const scrollLeft = () => {
  shortsContainer.value?.scrollBy({
    left: -300,
    behavior: 'smooth'
  })
}

const scrollRight = () => {
  shortsContainer.value?.scrollBy({
    left: 300,
    behavior: 'smooth'
  })
}
const video_placeholder = "https://videos.pexels.com/video-files/28926280/12519177_1920_1080_30fps.mp4"
const video_placegolder_vert = "https://videos.pexels.com/video-files/9512228/9512228-uhd_1440_2732_25fps.mp4"
</script>