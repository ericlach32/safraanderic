<script setup>
import { onMounted } from 'vue'
import Hero from '../components/Hero.vue'
import ImageAndCopy from '../components/ImageAndCopy.vue'
import ImageCarousel from '../components/ImageCarousel.vue'
import Faq from '../components/Faq.vue'
import Countdown from '@/components/Countdown.vue';
import ContactForm from '@/components/ContactForm.vue';

// Handle smooth scrolling for data-scroll-to links
onMounted(() => {
  const scrollToLinks = document.querySelectorAll('[data-scroll-to]')
  
  scrollToLinks.forEach(link => {
    link.addEventListener('click', (e) => {
      e.preventDefault()
      const targetId = link.getAttribute('href')
      const targetElement = document.querySelector(targetId)
      
      if (targetElement) {
        // Use smooth scrolling without router animation conflicts
        targetElement.scrollIntoView({
          behavior: 'smooth',
          block: 'start'
        })
      }
    })
  })
})
</script>

<template>
  <div class="container">
    <Hero
      heading="About Us"
      subheading="Now & Forever"
      imageUrl="/fall-canal.jpg"
      imageAlt="Stonefields Estate"
      imageMobileUrl="/fall-canal.jpg"
      imageMobileAlt="Stonefields Estate"
      :fullHeight="false"
      mobilePosition="top"
      desktopPosition="left"
      customClass="hero--about"
    />
    <Countdown />
    <!-- <ImageAndCopy
      heading="Our Story"
      subheading="We're simply meant to be."
      copy="<p>You know something? We are really cool and you know it. I know you know it. We're really really cool and you know it. We're really cool and you know it. We're really cool and you know it. I know it, yes I do. We're really cool and you know it. We're unbelievably really cool and you know it. We're <b>really cool</b> and you know it. We're really cool and you know it.</p>"
      imageUrl="/safra-and-eric-bw.jpg"
      imageAlt="Safra and Eric"
      imageMobileUrl="/safra-and-eric-bw.jpg"
      imageMobileAlt="Safra and Eric"
      mobilePosition="bottom"
      desktopPosition="right"
    /> -->
    <ImageAndCopy
      heading="Our Story"
      subheading="We're simply meant to be."
      copy="<p>You know something? We are really cool and you know it. I know you know it. We're really really cool and you know it. We're really cool and you know it. We're really cool and you know it. I know it, yes I do. We're really cool and you know it. We're unbelievably really cool and you know it. We're <b>really cool</b> and you know it. We're really cool and you know it.</p>"
      imageUrl="/safra-and-eric-bw.jpg"
      imageAlt="Safra and Eric"
      imageMobileUrl="/safra-and-eric-bw.jpg"
      imageMobileAlt="Safra and Eric"
      mobilePosition="top"
      desktopPosition="right"
    />
    <ImageCarousel
      imageUrl="/safra-and-eric-heads.jpg"
      image2Url="/safra-and-eric-dark-stairs.jpg"
      image3Url="/safra-and-eric-hands.jpg"
      imageAlt="Safra and Eric"
    />
    <div class="faq">
      <div class="faq__header">
        <h2>Frequently Asked Questions</h2>
      </div>
      <div class="faq__content">
        <Faq 
          question="Is the wedding going to be spooky? What are the vibes?"
          answer="<p>Yes… but make it elegant. Expect subtle Halloween vibes – not jump scares. Think candlelight, autumn air, rich colours, and gothic touches. If you’re picturing a haunted house, you’re in the wrong movie genre – think Tim Burton meets romance novel.</p>"
        />
        <Faq 
          question="Should I be planning on wearing a costume for this Halloween wedding?"
          answer="<p>Nope! While it’s a Halloween wedding, it’s not a costume party. Please save the full-on costumes for another time – we’ll have a dress code to guide your outfit choices once invites go out. (Spoiler: think moody, romantic, and a little glam)</p>"
        />
        <Faq 
          question="What is the dress code?"
          answer="<p>Our dress code is formal. We suggest that men wear a suit in any colour and women wear a long formal dress.</p>"
        />
        <Faq 
          question="Can I wear black?"
          answer="<p>Absolutely. Black, deep jewel tones, and dramatic fabrics are totally welcome – and encouraged.</p>"
        />
        <Faq 
          question="What colours should I avoid wearing?"
          answer="<p>We will be having a multi-cultural wedding, the bride will be wearing a white dress with red accessories. Red in Pakistani weddings symbolizes love, prosperity, and new beginnings. Please refrain from wearing red or white.</p><p>Our bridesmaids will be in burnt orange. Please also refrain from wearing a long dress in that colour.</p>"
        />
        <Faq 
          question="Will all events be in the same location?"
          answer="<p>Yes, the ceremony and reception will be in the same venue. We’ll share the exact address and timing with the invitation. This information will be added to the website once the invitations go out.</p>"
        />
        <Faq 
          question="Should I start booking flights or accommodation now?"
          answer="<p>Yes, especially if you’re flying in or coming from out of town. It’s a popular time of year so we recommend booking flights and accommodations early to get the best rates.</p>"
        />
        <Faq 
          question="Are there hotel blocks or suggested places to stay?"
          answer="<p>Yes, please see <a href='#'>Accommodations / Travel</a>.</p>"
        />
        <Faq 
          question="What’s the closest airport / train station?"
          answer="<p>The closest airport is Ottawa International Airport (YOW) – about an hour’s drive from the venue.</p><p>The closest train station is Ottawa Train Station – about an hour’s drive from the venue.</p><p>For more information, see <a href='#'>Accommodations / Travel</a>.</p>"
        />
        <Faq 
          question="Is there transportation to and from the venue?"
          answer="<p>Yes there will be a shuttle between the two hotels and the venue, we will include transportation information with the invitation and on the website after the invitations are out.</p>"
        />
        <Faq 
          question="Can I bring a plus one?"
          answer="<p>Your invitation will specify if you have a plus one. We appreciate your understanding that our guest list is limited to those explicitly named on the invitation.</p>"
        />
        <Faq 
          question="Are kids invited?"
          answer="<p>We love your little ones, but this will be an adults-only celebration with the exception of close cousins. Your Invitation reflects exactly who is invited, we hope this gives parents a chance to relax and enjoy a night out.</p>"
        />
        <Faq 
          question="When will wedding invitations come out?"
          answer="<p>Invitations will be sent between May and June 2026 and will include everything you need to RSVP, choose your meal, and plan your outfits.</p>"
        />
        <Faq 
          question="What should I do if I know I can’t attend now?"
          answer="<p>We will miss you! If you already know you will not be able to join us, feel free to reach out early so we can plan accordingly. You can contact us <a href='#contact-form' data-scroll-to>here</a> or at <a href='mailto:ericandsafra2026@gmail.com'>ericandsafra2026@gmail.com</a>.</p>"
        />
        <Faq 
          question="Can I request a specific meal or note dietary restrictions?"
          answer="<p>Yes! When you RSVP, you’ll be able to note any dietary restrictions or allergies. All meat served will be <b>halal</b>, and we’ll have vegetarian options as well. We want everyone to feel taken care of.</p>"
        />
        <Faq 
          question="Will there be alcohol?"
          answer="<p>Yes! There will be a full bar, along with signature drinks to help keep the spirits high all night long.</p>"
        />
        <Faq 
          question="I have a question not answered here; how do I contact you?"
          answer="<p>Feel free to email us at <a href='mailto:ericandsafra2026@gmail.com'>ericandsafra2026@gmail.com</a> or contact us here. We’re happy to help with anything you’re unsure about.</p>"
        />
      </div>
    </div>
    <ContactForm />
  </div>
</template>
