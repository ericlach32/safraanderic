<script setup>
import { onMounted, nextTick } from 'vue'

defineProps({
  imageUrl: {
    type: String,
    required: false,
  },
  image2Url: {
    type: String,
    required: false,
  },
  image3Url: {
    type: String,
    required: false,
  },
  image4Url: {
    type: String,
    required: false,
  },
  imageAlt: {
    type: String,
    required: false,
  },
})

let swiper = null

onMounted(async () => {
  // Wait for DOM to be fully rendered
  await nextTick()
  
  // Initialize Swiper
  swiper = new Swiper('.swiper', {
    slidesPerView: 'auto',
    spaceBetween: 24,
    // centeredSlides: true,
    // loop: true,
    // autoplay: {
    //   delay: 7000,
    //   disableOnInteraction: false,
    // },
    pagination: {
      el: '.swiper-pagination',
      clickable: true,
    },
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },
    breakpoints: {
      768: {
        // slidesPerView: 1,
        // spaceBetween: 32,
      },
    },
  })
})
</script>

<template>
  <div class="image-carousel">
    <div class="swiper">
      <div class="swiper-wrapper">
        <div class="swiper-slide">
          <div class="image-carousel__slide">
            <img
              v-if="imageUrl"
              :src="imageUrl"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide">
          <div class="image-carousel__slide">
            <img
              v-if="image2Url"
              :src="image2Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide">
          <div class="image-carousel__slide">
            <img
              v-if="image3Url"
              :src="image3Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
      </div>
      <div class="swiper-pagination"></div>
      <div class="swiper-button-prev"></div>
      <div class="swiper-button-next"></div>
    </div>
  </div>
</template>
