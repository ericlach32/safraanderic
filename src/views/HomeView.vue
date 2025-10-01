<script setup>
import Hero from '../components/Hero.vue'
import ImageAndCopy from '../components/ImageAndCopy.vue'
import ImageCarousel from '../components/ImageCarousel.vue'
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
      <ImageAndCopy
        heading="Our Story"
        subheading="We're simply meant to be."
        copy="<p>You know something? We are really cool and you know it. I know you know it. We're really really cool and you know it. We're really cool and you know it. We're really cool and you know it. I know it, yes I do. We're really cool and you know it. We're unbelievably really cool and you know it. We're <b>really cool</b> and you know it. We're really cool and you know it.</p>"
        imageUrl="/safra-and-eric-ny-1.jpg"
        imageAlt="Safra and Eric"
        imageMobileUrl="/safra-and-eric-ny-1.jpg"
        imageMobileAlt="Safra and Eric"
        mobilePosition="top"
        desktopPosition="right"
      />
      <ImageCarousel
        imageUrl="/safra-and-eric-ny-3.jpg"
        image2Url="/safra-and-eric-ny-2.jpg"
        image3Url="/safra-and-eric-ny-4.jpg"
        imageAlt="Safra and Eric"
      />
    </div>
  </main>
</template>
