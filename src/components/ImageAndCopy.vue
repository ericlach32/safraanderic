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
  copy: {
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
    class="image-and-copy"
    :class="[
      customClass,
      { 'image-and-copy--full-height': fullHeight },
      mobilePosition ? `image-and-copy--mobile-${mobilePosition}` : 'image-and-copy--mobile-center',
      desktopPosition ? `image-and-copy--desktop-${desktopPosition}` : 'image-and-copy--desktop-center'
    ]">
    <div class="image-and-copy__container">
      <div class="image-and-copy__content">
        <h2>{{ heading }}</h2>
        <h3>{{ subheading }}</h3>
        <p v-html="copy"></p>
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
