<script setup>
defineProps({
  heading: {
    type: String,
    required: true,
  },
  subheading: {
    type: String,
    required: true,
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
  fullHeight: {
    type: Boolean,
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
    class="hero"
    :class="[
      customClass,
      { 'hero--full-height': fullHeight },
      mobilePosition ? `hero--mobile-${mobilePosition}` : 'hero--mobile-center',
      desktopPosition ? `hero--desktop-${desktopPosition}` : 'hero--desktop-center'
    ]">
    <div class="hero__content">
      <h1>{{ heading }}</h1>
      <h2>{{ subheading }}</h2>
    </div>
    <img 
      v-if="imageUrl"
      :src="imageUrl"
      :alt="imageAlt"
      class="hero__image hero__image--desktop"
    />
    <img 
      v-if="imageMobileUrl"
      :src="imageMobileUrl"
      :alt="imageMobileAlt"
      class="hero__image hero__image--mobile"
    />
  </div>
</template>
