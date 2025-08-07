<script setup>
import Hero from '../components/Hero.vue'
import Faq from '../components/Faq.vue'
import Countdown from '@/components/Countdown.vue';
import ContactForm from '@/components/ContactForm.vue';
</script>

<template>
  <div class="container">
    <Hero
      heading="About Us!"
      subheading="We tha shit."
      imageUrl="/aframe-1.jpg"
      imageAlt="Stonefields Estate"
      imageMobileUrl="/aframe-3.jpg"
      imageMobileAlt="Stonefields Estate"
      :fullHeight="false"
      mobilePosition="top"
      desktopPosition="left"
    />
    <Countdown />
    <ContactForm />
    <div class="faq">
      <div class="faq__header">
        <h2>FAQ</h2>
      </div>
      <div class="faq__content">
        <Faq 
          question="Do you like us?" 
          answer="Well you better. If you don't then why are you even on here? Get a life." 
        />
        <Faq 
          question="This is another question?" 
          answer="Lorem ipsum dolor sit amet consectetur adipisicing elit. Quidem, eveniet numquam quaerat vel, odio quis perspiciatis exercitationem repellendus ex voluptate molestias est nisi sit. Fuga fugiat in minus consequatur repellendus." 
        />
        <Faq 
          question="What is happening?" 
          answer="Lorem ipsum dolor sit amet consectetur adipisicing elit. Quidem labore itaque porro, qui quod corrupti eligendi sint inventore eveniet modi ex aspernatur repudiandae veritatis optio deleniti voluptatem doloremque ipsam natus!" 
        />
        <Faq 
          question="Why are there so many questions?" 
          answer="Lorem ipsum, dolor sit amet consectetur adipisicing elit. Ipsam aliquam vitae ipsa, enim natus dolorem eligendi delectus optio inventore cupiditate possimus rem, animi quibusdam nemo aut. Blanditiis nemo fugiat minima." 
        />
      </div>
    </div>
  </div>
</template>
