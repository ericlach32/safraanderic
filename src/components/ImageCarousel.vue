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
  image5Url: {
    type: String,
    required: false,
  },
  image6Url: {
    type: String,
    required: false,
  },
  image7Url: {
    type: String,
    required: false,
  },
  image8Url: {
    type: String,
    required: false,
  },
  image9Url: {
    type: String,
    required: false,
  },
  image10Url: {
    type: String,
    required: false,
  },
  image11Url: {
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
    mousewheel: {
      forceToAxis: true,
    },
    // centeredSlides: true,
    // loop: true,
    // autoplay: {
    //   delay: 7000,
    //   disableOnInteraction: false,
    // },
    pagination: {
      el: '.swiper-pagination',
      clickable: true,
      dynamicBullets: false,
      renderBullet: function (index, className) {
        return '<span class="' + className + '"></span>';
      },
    },
    navigation: {
      nextEl: '.swiper-button-next',
      prevEl: '.swiper-button-prev',
    },
    on: {
      slideChange: function () {
        // Force pagination update on slide change
        this.pagination.render();
        this.pagination.update();
      },
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
        <div class="swiper-slide" v-if="imageUrl">
          <div class="image-carousel__slide">
            <img
              v-if="imageUrl"
              :src="imageUrl"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image2Url">
          <div class="image-carousel__slide">
            <img
              v-if="image2Url"
              :src="image2Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image3Url">
          <div class="image-carousel__slide">
            <img
              v-if="image3Url"
              :src="image3Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image4Url">
          <div class="image-carousel__slide">
            <img
              v-if="image4Url"
              :src="image4Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image5Url">
          <div class="image-carousel__slide">
            <img
              v-if="image5Url"
              :src="image5Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image6Url">
          <div class="image-carousel__slide">
            <img
              v-if="image6Url"
              :src="image6Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image7Url">
          <div class="image-carousel__slide">
            <img
              v-if="image7Url"
              :src="image7Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image8Url">
          <div class="image-carousel__slide">
            <img
              v-if="image8Url"
              :src="image8Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image9Url">
          <div class="image-carousel__slide">
            <img
              v-if="image9Url"
              :src="image9Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image10Url">
          <div class="image-carousel__slide">
            <img
              v-if="image10Url"
              :src="image10Url"
              :alt="imageAlt"
              class="image-carousel__image"
            />
          </div>
        </div>
        <div class="swiper-slide" v-if="image11Url">
          <div class="image-carousel__slide">
            <img
              v-if="image11Url"
              :src="image11Url"
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
