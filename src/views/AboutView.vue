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
    question: "Can I bring a plus one?",
    answer: "<p>Your invitation will specify if you have a plus one. We appreciate your understanding that our guest list is limited to those explicitly named on the invitation.</p>"
  },
  {
    question: "Are kids invited?",
    answer: "<p>We love your little ones, but this will be an adults-only celebration with the exception of close cousins.</p>"
  },
  {
    question: "Are there hotel blocks or suggested places to stay?",
    answer: "<p>Yes, please see <a href='#accommodations' data-scroll-to>Accommodations / Travel</a>.</p>"
  },
  {
    question: "Is there transportation to and from the venue?",
    answer: "<p>Yes, please see <a href='#shuttle' data-scroll-to>Shuttle / Parking</a>.</p>"
  },
  {
    question: "What is the dress code?",
    answer: "<p>Dressy cocktail attire. Guests are welcome to wear Western or South Asian attire</p><p>Think suits (no tuxedos), cocktail to full-length dresses, saris, lehengas, and other polished, festive looks.</p><p>As our venue is mostly grass, we recommend avoiding stilettos. Block heels, wedges, or flats will be the most comfortable choice.</p>"
  },
  {
    question: "Should I be planning on wearing a costume for this Halloween wedding?",
    answer: "<p>No costumes, please! Think moody, romantic, and a little glam instead.</p>"
  },
  {
    question: "What colours should I avoid wearing?",
    answer: "<p>We kindly ask guests to avoid white, red, and champagne.</p><p>Bridesmaids will be in burnt orange long dresses and groomsmen in solid black, so please also avoid outfits or styling that closely match these looks.</p>"
  },
  {
    question: "Will all events be in the same location?",
    answer: "<p>Yes, the ceremony and reception will be in the same venue.</p>"
  },
  // {
  //   question: "Can I wear black?",
  //   answer: "<p>Absolutely. Black, deep jewel tones, and dramatic fabrics are totally welcome – and encouraged.</p>"
  // },
  {
    question: "Should I start booking flights or accommodation now?",
    answer: "<p>Yes, especially if you're flying in or coming from out of town. It's a popular time of year so we recommend booking flights and accommodations early to get the best rates.</p>"
  },
  {
    question: "What's the closest airport / train station?",
    answer: "<p>The closest airport is Ottawa International Airport (YOW) – about an hour's drive from the venue.</p><p>The closest train station is Ottawa Train Station – about an hour's drive from the venue.</p><p>For more information, see <a href='#accommodations' data-scroll-to>Accommodations / Travel</a>.</p>"
  },
  // {
  //   question: "What should I do if I know I can't attend now?",
  //   answer: "<p>We will miss you! If you already know you will not be able to join us, feel free to reach out early so we can plan accordingly. You can contact us <a href='#contact-form' data-scroll-to>here</a> or at <a href='mailto:ericandsafra2026@gmail.com'>ericandsafra2026@gmail.com</a>.</p>"
  // },
  // {
  //   question: "Can I request a specific meal or note dietary restrictions?",
  //   answer: "<p>Yes! When you RSVP, you'll be able to note any dietary restrictions or allergies. All meat served will be <b>halal</b>, and we'll have vegetarian options as well. We want everyone to feel taken care of.</p>"
  // },
  {
    question: "Will the food be halal?",
    answer: "<p>Yes! All meat served will be halal, there will be vegetarian options as well.</p>"
  },
  {
    question: "Will there be alcohol?",
    answer: "<p>Yes, a cash bar will be available throughout the evening, along with signature drinks to help keep the spirits high all night long.</p>"
  },
  {
    question: "When is the RSVP deadline?",
    answer: "<p>Please RSVP by <b>August 1st</b> via the response card in your invite.</p>"
  },
  {
    question: "When should I arrive at the venue?",
    answer: "<p>Please arrive between <b>3:15 p.m.</b> and <b>3:50 p.m.</b></p>"
  },
  {
    question: "Is there parking at the venue?",
    answer: "<p>Yes, there is ample parking available at the venue.</p>"
  },
  {
    question: "Do you have a registry?",
    answer: "<p>We do not have a registry. The greatest gift of all is your presence on our special day! However, should you wish to contribute to a deposit on our first home, a wedding card can be dropped in the card box at the reception.</p>"
  },
  {
    question: "Is the wedding going to be spooky? What are the vibes?",
    answer: "<p>Yes… but make it elegant. Expect subtle Halloween vibes – not jump scares. Think candlelight, autumn air, rich colours, and gothic touches. If you're picturing a haunted house, you're in the wrong movie genre – think Tim Burton meets romance novel.</p>"
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
    <ImageAndCopy
      heading="Our Venue"
      subheading="Stonefields Estate"
      copy="<p>Stonefields Estate is located approximately 30 minutes west of Ottawa at <a href='https://maps.app.goo.gl/ozpGg39BCWWUzFMH6' target='_blank'>1985 9th Line, Beckwith, ON, K7C 3P2</a>.</p><p><b>The ceremony will begin promptly at 4:00 p.m.</b> Guests may arrive beginning at 3:15 p.m. Late arrivals will not be admitted once the ceremony has begun.</p><p>Free on-site parking is available, and overnight parking is permitted. Vehicles left overnight must be picked up by noon the following day. If you plan to drink, we strongly encourage you to use the shuttle service, as taxi and ride-share options in the area are very limited. Please indicate whether you will be using the shuttle when you RSVP.</p><p>The ceremony and dinner will be held indoors, while cocktail hour will take place outdoors, weather permitting. Please note that walking on grass and gravel will be required.</p>"
      imageUrl="/stonefields-safra-and-eric.jpg"
      imageAlt="Safra and Eric"
      imageMobileUrl="/stonefields-safra-and-eric.jpg"
      imageMobileAlt="Safra and Eric"
      mobilePosition="top"
      desktopPosition="left"
    />
    <Map
      name="Stonefields Estate"
      address="1985 9th Line, Beckwith, ON K7C 3P2"
      open-info-on-load
    />
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
      copy="<p>We’ve reserved a block of rooms under Eric & Safra at <b>$220 per night</b>.</p><p>Room options include:</p><ul><li>1 King Bed</li><li>2 Queen Beds</li></ul><p>This hotel is ideal for guests driving to the wedding. If you’re flying or taking the train in, this hotel is not recommended, as rideshares and taxis in town are very limited.</p><p>A shuttle will take you to the wedding and bring you back afterward, so you can celebrate worry-free.</p><p>Online booking is open now: <a href='https://www.choicehotels.com/en-ca/reservations/groups/rv92a2' target='_blank'>https://www.choicehotels.com/en-ca/reservations/groups/rv92a2</a>.</p><p>Or you can book by phone at <a href='tel:6132160079'>(613) 216-0079</a>. Ask for a room under the Eric & Safra wedding block.</p>"
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
      copy="<p><b>By Car: </b>From Toronto, the drive to Beckwith/Carleton Place is about 4.5 hours. The most direct route is along Highway 401 East toward Ottawa, then Highway 416 North to Highway 417 West, and finally Highway 7 West to Carleton Place. Parking is available at both hotels as well as onsite at the venue, with the option to leave your car overnight.</p><p><b>By Plane: </b>The closest airport is Ottawa/Macdonald–Cartier International Airport (YOW). Direct flights are available from Toronto with Air Canada, Porter, and WestJet.</p><p>For our international guests, please note that Ottawa’s airport is smaller than most. You will likely need to connect through Toronto or Montreal to reach Ottawa.</p><p><b>By Train: </b>Via Rail offers services from Toronto to Ottawa, with the journey taking around 4.5 hours. From Ottawa’s train station, Beckwith/Carleton Place is about a 45-minute drive, so you will need to arrange a car rental or taxi / rideshare to reach your hotel or the venue.</p>"
      imageUrl="/safra-and-eric-vertical-stairs.jpg"
      imageAlt="Safra and Eric"
      imageMobileUrl="/safra-and-eric-vertical-stairs.jpg"
      imageMobileAlt="Safra and Eric"
      mobilePosition="bottom"
      desktopPosition="right"
    />

    <!-- TODO: Shuttle -->
    <div class="shuttle">
      <div class="shuttle__header">
        <h2 id="shuttle">Shuttle / Parking</h2>
      </div>
      <div class="shuttle__content">

        <div class="shuttle__intro">
          <p>There is plenty of parking at Stonefields Estate, with overnight parking available. If parking at the venue overnight, please pick up your vehicle by <b>12:00 p.m.</b> the following morning.</p>
          <!-- <p>We love you too much to let you drive after a night on the dance floor – please take the shuttle if you plan to drink. </p> -->
        </div>

        <div class="shuttle__subheading">
          <h3>Getting to the Venue</h3>
          <!-- <p>Parking is available at Stonefields Estate for guests who prefer to drive.</p> -->
        </div>

        <div class="shuttle__schedule">
          <div class="shuttle__schedule-block">
            <h4>Shuttle #1</h4>
            <ul>
              <li><b>2:45 p.m.</b> Pick-up: Homewood Suites by Hilton, 900 Great Lakes Avenue Kanata, ON, K2K 0L4</li>
              <li><b>3:15 p.m.</b> Pick-up: Comfort Inn & Suites, 355 McNeely Avenue Carleton Place, ON, K7C 0A1</li>
              <li><b>3:30 p.m.</b> Drop-off: Stonefields Estate</li>
            </ul>
          </div>
          <div class="shuttle__schedule-block">
            <h4>Shuttle #2</h4>
            <ul>
              <li><b>3:00 p.m.</b> Pick-up: Homewood Suites by Hilton, 900 Great Lakes Avenue Kanata, ON, K2K 0L4</li>
              <li><b>3:30 p.m.</b> Pick-up: Comfort Inn & Suites, 355 McNeely Avenue Carleton Place, ON, K7C 0A1</li>
              <li><b>3:40 p.m.</b> Drop-off: Stonefields Estate</li>
            </ul>
          </div>
        </div>

        <div class="shuttle__subheading">
          <h3>Leaving the Venue</h3>
          <!-- <p>Parking is available at Stonefields Estate for guests who prefer to drive.</p> -->
        </div>

        <div class="shuttle__schedule">
          <div class="shuttle__schedule-block">
            <h4>Shuttle #1</h4>
            <ul>
              <li><b>11:00 p.m.</b> Departure from Stonefields Estate</li>
              <li><b>11:10 p.m.</b> Drop-off: Comfort Inn & Suites, Carleton Place, ON</li>
              <li><b>11:30 p.m.</b> Drop-off: Homewood Suites by Hilton, Kanata, ON</li>
            </ul>
          </div>
          <div class="shuttle__schedule-block">
            <h4>Shuttle #2 & #3</h4>
            <ul>
              <li><b>12:45 a.m.</b> Departure from Stonefields Estate</li>
              <li><b>12:55 a.m.</b> Drop-off: Comfort Inn & Suites, Carleton Place, ON</li>
              <li><b>1:15 a.m.</b> &nbsp;&nbsp;Drop-off: Homewood Suites by Hilton, Kanata, ON</li>
            </ul>
          </div>
        </div>

        <div class="shuttle__outro">
          <p>Shuttles will depart on time and cannot wait for late guests. No stops will be made between&nbsp;locations.</p>
        </div>

      </div>
    </div>

    <!-- TODO: Schedule -->

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
    <ContactForm />
    <div class="footer">
      <p>Safra & Eric</p>
    </div>
  </div>
</template>
