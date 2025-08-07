<script setup>
import Hero from '../components/Hero.vue'
</script>

<template>
  <main>
    <div class="container">
      <Hero
        heading="Eric and Safra"
        subheading="2026"
        imageUrl="/stonefields-2.jpg"
        imageAlt="Stonefields Estate"
        imageMobileUrl="/stonefields-3.jpg"
        imageMobileAlt="Stonefields Estate"
        :fullHeight="true"
        mobilePosition="bottom"
        desktopPosition="right"
      />
    </div>
  </main>
</template>
