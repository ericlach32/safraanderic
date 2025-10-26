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
    answer: "<p>We will be having a multi-cultural wedding, the bride will be wearing a white dress with red accessories. Red in Pakistani weddings symbolizes love, prosperity, and new beginnings. Please refrain from wearing white or champagne.</p><p>Our bridesmaids will be in burnt orange. Please also refrain from wearing a long dress in that colour.</p>"
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
    answer: "<p>We love your little ones, but this will be an adults-only celebration with the exception of close cousins. Your invitation reflects exactly who is invited, we hope this gives parents a chance to relax and enjoy a night out.</p>"
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
      copy="<p>We’ve reserved a block of rooms under Eric & Safra at <b>$220 per night</b>.</p><p>Room options include:</p><ul><li>1 King Bed</li><li>2 Queen Beds</li></ul><p>This hotel is ideal for guests driving to the wedding. If you’re flying or taking the train in, this hotel is not recommended, as rideshares and taxis in town are very limited.</p><p>A shuttle will take you to the wedding and bring you back afterward, so you can celebrate worry-free.</p><p>Online booking opens <b>November 16, 2025</b>.</p><p>If you’d like to book before then, you can book by phone at <a href='tel:6132160079'>(613) 216-0079</a>. Ask for a room under the Eric & Safra wedding block.</p>"
      name="Comfort Inn & Suites"
      address="355 McNeely Ave, Carleton Place, ON K7C 0A1"
    />
    <Map
      heading="Homewood Suites by Hilton"
      subheading="900 Great Lakes Ave, Kanata, ON"
      copy="<p>We’ve reserved a block of suites under Eric & Safra at <b>15% off per night</b>.</p><p>All rooms are spacious suites with full kitchens and fridges. Options include:</p><ul><li>2 Queen Beds</li><li>1 King Bed</li><li>2-Room Suites</li></ul><p>This hotel is recommended for guests taking the train or flying in. You cannot get an Uber or Lyft to the Carleton Place hotel from Ottawa and taxis are limited coming out of Carleton Place. There are plenty of shops and restaurants within walking distance from the hotel.</p><p>A shuttle will take you to the wedding and bring you back to the hotel afterward, so you can celebrate worry-free.</p><p>Online booking is open now: <a href='https://group.homewood-suites.com/myrf6s' target='_blank'>https://group.homewood-suites.com/myrf6s</a></p>"
      name="Homewood Suites by Hilton"
      address="900 Great Lakes Ave, Kanata, ON K2K 0L4"
    />
    <ImageAndCopy
      customClass="image-and-copy__container--vertical-stairs"
      heading="Getting There"
      copy="<p><b>By Car: </b>From Toronto, the drive to Beckwith/Carleton Place is about 4.5 hours. The most direct route is along Highway 401 East toward Ottawa, then Highway 416 North, and finally Highway 7 West to Carleton Place. Parking is available at both hotels as well as onsite at the venue, with the option to leave your car overnight.</p><p><b>By Plane: </b>The closest airport is Ottawa/Macdonald–Cartier International Airport (YOW). Direct flights are available from Toronto with Air Canada, Porter, and WestJet.</p><p>For our international guests, please note that Ottawa’s airport is smaller than most. You will likely need to connect through Toronto or Montreal to reach Ottawa.</p><p><b>By Train: </b>Via Rail offers services from Toronto to Ottawa, with the journey taking around 4.5 hours. From Ottawa’s train station, Beckwith/Carleton Place is about a 45-minute drive, so you will need to arrange a car rental or taxi / rideshare to reach your hotel or the venue.</p>"
      imageUrl="/safra-and-eric-vertical-stairs.jpg"
      imageAlt="Safra and Eric"
      imageMobileUrl="/safra-and-eric-vertical-stairs.jpg"
      imageMobileAlt="Safra and Eric"
      mobilePosition="bottom"
      desktopPosition="right"
    />
    <ContactForm />
    <div class="footer">
      <p>Safra & Eric</p>
    </div>
  </div>
</template>
