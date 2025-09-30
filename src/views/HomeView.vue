<script setup>
import Hero from '../components/Hero.vue'
</script>

<template>
  <main>
    <div class="container">
      <Hero
        heading="Safra and Eric"
        subheading="Beckwith, 2026"
        imageUrl="/safra-and-eric-hero-d.jpg"
        imageAlt="Safra and Eric"
        imageMobileUrl="/safra-and-eric-hero-m.jpg"
        imageMobileAlt="Safra and Eric"
        :fullHeight="true"
        mobilePosition="bottom"
        desktopPosition="right"
        customClass="hero--stairs"
      />
    </div>
  </main>
</template>
