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
        copy="<p>Safra and Eric’s story began in September 2021, when they first connected over a shared love of music and movies (shoutout to <i>The Turning Point</i>). On Halloween night, while watching John Carpenter’s <i>Halloween</i>, Eric asked Safra to be his partner. From that moment, they’ve been inseparable.</p><p>Five years after that first Halloween together, they will say “I do” on October 31, 2026 in Beckwith, Ontario, surrounded by the love of family and friends.</p>"
        ctaUrl="/about"
        ctaText="Learn More"
        imageUrl="/safra-and-eric-ny-1.jpg"
        imageAlt="Safra and Eric"
        imageMobileUrl="/safra-and-eric-ny-1.jpg"
        imageMobileAlt="Safra and Eric"
        mobilePosition="top"
        desktopPosition="right"
      />
      <ImageCarousel
        imageUrl="/safra-and-eric-memory-1.jpg"
        image2Url="/safra-and-eric-memory-3.jpg"
        image3Url="/safra-and-eric-memory-2.jpg"
        image4Url="/safra-and-eric-memory-4.jpg"
        image5Url="/safra-and-eric-memory-5.jpg"
        image6Url="/safra-and-eric-memory-6.jpg"
        image7Url="/safra-and-eric-memory-7.jpg"
        image8Url="/safra-and-eric-memory-8.jpg"
        image9Url="/safra-and-eric-memory-9.jpg"
        image10Url="/safra-and-eric-memory-11.jpg"
        image11Url="/safra-and-eric-memory-10.jpg"
        imageAlt="Safra and Eric"
      />
      <div class="footer">
        <p>Safra & Eric</p>
      </div>
    </div>
  </main>
</template>
