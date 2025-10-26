<script setup>
// import Hero from '../components/Hero.vue'
// import Faq from '../components/Faq.vue'
import ImageAndCopy from '../components/ImageAndCopy.vue'
</script>

<template>
  <div>
    <div class="container container--full">
      
      <div class="colors">
        <div class="color" style="background: #101217;">
          <span style="color: #F7E6CA;">#101217</span>
        </div>
        <div class="color" style="background: #580000;">
          <span style="color: #F7E6CA;">#580000</span>
        </div>
        <div class="color" style="background: #904134;">
          <span style="color: #F7E6CA;">#904134</span>
        </div>
        <div class="color" style="background: #BC8410;">
          <span style="color: #FFFFFF;">#BC8410</span>
        </div>
        <div class="color" style="background: #F7E6CA;">
          <span style="color: #101217;">#F7E6CA</span>
        </div>
        <div class="color" style="background: #ECE2DD;">
          <span style="color: #101217;">#ECE2DD</span>
        </div>
      </div>
    
    </div>
    <div class="container container--no-height">
      <ImageAndCopy
        heading="Our Colors"
        subheading=""
        copy="<p>We will be having a multi-cultural wedding, the bride will be wearing a white dress with red accessories. Red in Pakistani weddings symbolizes love, prosperity, and new beginnings. Please refrain from wearing white or champagne.</p><p>Our bridesmaids will be in burnt orange. Please also refrain from wearing a long dress in that colour.</p><p>Black, deep jewel tones, and dramatic fabrics are totally welcome – and encouraged.</p>"
        imageUrl="/safra-and-eric-colors.jpg"
        imageAlt="Safra and Eric"
        imageMobileUrl="/safra-and-eric-colors.jpg"
        imageMobileAlt="Safra and Eric"
        mobilePosition="top"
        desktopPosition="right"
      />
    </div>
  </div>
</template>
