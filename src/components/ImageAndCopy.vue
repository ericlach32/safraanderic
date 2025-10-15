<script setup>
import { RouterLink } from 'vue-router'

defineProps({
  heading: {
    type: String,
    required: true,
  },
  subheading: {
    type: String,
    required: true,
  },
  copy: {
    type: String,
    required: true,
  },
  ctaUrl: {
    type: String,
    required: false,
  },
  ctaText: {
    type: String,
    required: false,
  },
  imageUrl: {
    type: String,
    required: false,
  },
  imageAlt: {
    type: String,
    required: false,
  },
  imageMobileUrl: {
    type: String,
    required: false,
  },
  imageMobileAlt: {
    type: String,
    required: false,
  },
  mobilePosition: {
    type: String,
    required: false,
  },
  desktopPosition: {
    type: String,
    required: false,
  },
  customClass: {
    type: String,
    required: false,
  },
})
</script>

<template>
  <div 
    class="image-and-copy">
    <div
      class="image-and-copy__container"
      :class="[
      customClass,
      mobilePosition ? `image-and-copy__container--mobile-${mobilePosition}` : 'image-and-copy__container--mobile-center',
      desktopPosition ? `image-and-copy__container--desktop-${desktopPosition}` : 'image-and-copy__container--desktop-center'
      ]">
      <div class="image-and-copy__content">
        <h2>{{ heading }}</h2>
        <h3 v-if="subheading">{{ subheading }}</h3>
        <div class="image-and-copy__copy" v-html="copy"></div>
        <RouterLink
          v-if="ctaUrl"
          v-html="ctaText"
          :to="ctaUrl"
          class="image-and-copy__cta btn">
        </RouterLink>
      </div>
      <div class="image-and-copy__image-wrapper">
        <img 
          v-if="imageUrl"
          :src="imageUrl"
          :alt="imageAlt"
          class="image-and-copy__image image-and-copy__image--desktop"
        />
        <img 
          v-if="imageMobileUrl"
          :src="imageMobileUrl"
          :alt="imageMobileAlt"
          class="image-and-copy__image image-and-copy__image--mobile"
        />
      </div>
    </div>
  </div>
</template>
