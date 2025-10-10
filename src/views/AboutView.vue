<script setup>
import { onMounted, ref, computed } from 'vue'
import Hero from '../components/Hero.vue'
import ImageAndCopy from '../components/ImageAndCopy.vue'
import ImageCarousel from '../components/ImageCarousel.vue'
import Faq from '../components/Faq.vue'
import Countdown from '@/components/Countdown.vue'
import ContactForm from '@/components/ContactForm.vue'
import Map from '@/components/Map.vue'

// FAQ expansion state
const showAllFaqs = ref(false)

// FAQ data
const faqData = [
  {
    question: "Is the wedding going to be spooky? What are the vibes?",
    answer: "<p>Yes… but make it elegant. Expect subtle Halloween vibes – not jump scares. Think candlelight, autumn air, rich colours, and gothic touches. If you're picturing a haunted house, you're in the wrong movie genre – think Tim Burton meets romance novel.</p>"
  },
  {
    question: "Should I be planning on wearing a costume for this Halloween wedding?",
    answer: "<p>Nope! While it's a Halloween wedding, it's not a costume party. Please save the full-on costumes for another time – we'll have a dress code to guide your outfit choices once invites go out. (Spoiler: think moody, romantic, and a little glam)</p>"
  },
  {
    question: "What is the dress code?",
    answer: "<p>Our dress code is formal. We suggest that men wear a suit in any colour and women wear a long formal dress.</p>"
  },
  {
    question: "Can I wear black?",
    answer: "<p>Absolutely. Black, deep jewel tones, and dramatic fabrics are totally welcome – and encouraged.</p>"
  },
  {
    question: "What colours should I avoid wearing?",
    answer: "<p>We will be having a multi-cultural wedding, the bride will be wearing a white dress with red accessories. Red in Pakistani weddings symbolizes love, prosperity, and new beginnings. Please refrain from wearing red or white.</p><p>Our bridesmaids will be in burnt orange. Please also refrain from wearing a long dress in that colour.</p>"
  },
  {
    question: "Will all events be in the same location?",
    answer: "<p>Yes, the ceremony and reception will be in the same venue. We'll share the exact address and timing with the invitation. This information will be added to the website once the invitations go out.</p>"
  },
  {
    question: "Should I start booking flights or accommodation now?",
    answer: "<p>Yes, especially if you're flying in or coming from out of town. It's a popular time of year so we recommend booking flights and accommodations early to get the best rates.</p>"
  },
  {
    question: "Are there hotel blocks or suggested places to stay?",
    answer: "<p>Yes, please see <a href='#accommodations' data-scroll-to>Accommodations / Travel</a>.</p>"
  },
  {
    question: "What's the closest airport / train station?",
    answer: "<p>The closest airport is Ottawa International Airport (YOW) – about an hour's drive from the venue.</p><p>The closest train station is Ottawa Train Station – about an hour's drive from the venue.</p><p>For more information, see <a href='#accommodations' data-scroll-to>Accommodations / Travel</a>.</p>"
  },
  {
    question: "Is there transportation to and from the venue?",
    answer: "<p>Yes there will be a shuttle between the two hotels and the venue, we will include transportation information with the invitation and on the website after the invitations are out.</p>"
  },
  {
    question: "Can I bring a plus one?",
    answer: "<p>Your invitation will specify if you have a plus one. We appreciate your understanding that our guest list is limited to those explicitly named on the invitation.</p>"
  },
  {
    question: "Are kids invited?",
    answer: "<p>We love your little ones, but this will be an adults-only celebration with the exception of close cousins. Your Invitation reflects exactly who is invited, we hope this gives parents a chance to relax and enjoy a night out.</p>"
  },
  {
    question: "When will wedding invitations come out?",
    answer: "<p>Invitations will be sent between May and June 2026 and will include everything you need to RSVP, choose your meal, and plan your outfits.</p>"
  },
  {
    question: "What should I do if I know I can't attend now?",
    answer: "<p>We will miss you! If you already know you will not be able to join us, feel free to reach out early so we can plan accordingly. You can contact us <a href='#contact-form' data-scroll-to>here</a> or at <a href='mailto:ericandsafra2026@gmail.com'>ericandsafra2026@gmail.com</a>.</p>"
  },
  {
    question: "Can I request a specific meal or note dietary restrictions?",
    answer: "<p>Yes! When you RSVP, you'll be able to note any dietary restrictions or allergies. All meat served will be <b>halal</b>, and we'll have vegetarian options as well. We want everyone to feel taken care of.</p>"
  },
  {
    question: "Will there be alcohol?",
    answer: "<p>Yes! There will be a full bar, along with signature drinks to help keep the spirits high all night long.</p>"
  },
  {
    question: "I have a question not answered here; how do I contact you?",
    answer: "<p>Feel free to email us at <a href='mailto:ericandsafra2026@gmail.com'>ericandsafra2026@gmail.com</a> or contact us <a href='#contact-form' data-scroll-to>here</a>. We're happy to help with anything you're unsure about.</p>"
  }
]

// Computed property to show limited or all FAQs
const displayedFaqs = computed(() => {
  return showAllFaqs.value ? faqData : faqData.slice(0, 5)
})

// Toggle function
const toggleFaqs = () => {
  showAllFaqs.value = !showAllFaqs.value
}

// Handle smooth scrolling for data-scroll-to links
const handleScrollToClick = (e) => {
  e.preventDefault()
  const targetId = e.target.getAttribute('href')
  const targetElement = document.querySelector(targetId)
  
  if (targetElement) {
    // Use smooth scrolling without router animation conflicts
    targetElement.scrollIntoView({
      behavior: 'smooth',
      block: 'start'
    })
  }
}

onMounted(() => {
  // Use event delegation to handle dynamically rendered links
  document.addEventListener('click', (e) => {
    if (e.target.hasAttribute('data-scroll-to')) {
      handleScrollToClick(e)
    }
  })
})
</script>

<template>
  <div class="container">
    <Hero
      heading="Information"
      subheading="Be Our Guest"
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
    <ImageAndCopy
      heading="Our Wedding"
      subheading="Now & Forever"
      copy="<p>On November 1, 2024, Eric proposed to Safra in New York while they were dressed as Jack and Sally from The Nightmare Before Christmas.</p><p>As the countdown to the wedding begins, they’d love for you to be part of this celebration. Below you’ll find everything you need to know about the wedding weekend – where to stay, what to expect, and how the celebrations will unfold.</p>"
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
          v-for="faq in displayedFaqs"
          :key="faq.question"
          :question="faq.question"
          :answer="faq.answer"
        />
        <div class="faq__toggle">
          <button 
            @click="toggleFaqs"
            class="btn">
            <span v-if="!showAllFaqs">Read More FAQs</span>
            <span v-else>Show Less</span>
          </button>
        </div>
      </div>
    </div>
    <ImageCarousel
      imageUrl="/safra-and-eric-ny-3.jpg"
      image2Url="/safra-and-eric-ny-2.jpg"
      image3Url="/safra-and-eric-ny-4.jpg"
      imageAlt="Safra and Eric"
    />
    <Map
      header="Accommodations / Travel"
      heading="Comfort Inn & Suites"
      subheading="355 McNeely Ave, Carleton Place, ON"
      name="Comfort Inn & Suites"
      address="355 McNeely Ave, Carleton Place, ON K7C 0A1"
    />
    <ContactForm />
  </div>
</template>
