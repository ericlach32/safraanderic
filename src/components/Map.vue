<script setup>
import { onMounted, ref, watch, nextTick } from 'vue'

const props = defineProps({
  header: {
    type: String
  },
  heading: {
    type: String
  },
  subheading: {
    type: String
  },
  address: {
    type: String,
    required: true,
    default: 'New York, NY'
  },
  zoom: {
    type: Number,
    default: 14
  },
  mapTypeId: {
    type: String,
    default: 'roadmap',
    validator: (value) => ['roadmap', 'satellite', 'hybrid', 'terrain'].includes(value)
  },
  apiKey: {
    type: String,
    default: 'AIzaSyCzcXX1r10Q93mvF2bSVkrASk5bLP5EzKU'
  },
})

const mapContainer = ref(null)
const map = ref(null)
const marker = ref(null)
const geocoder = ref(null)
const isLoading = ref(true)
const error = ref(null)

// Load Google Maps API
const loadGoogleMapsAPI = () => {
  return new Promise((resolve, reject) => {    
    if (window.google && window.google.maps) {
      resolve()
      return
    }

    const script = document.createElement('script')
    script.src = `https://maps.googleapis.com/maps/api/js?key=${props.apiKey}&libraries=places`
    script.async = true
    script.defer = true
    
    script.onload = () => {
      console.log('Google Maps API loaded successfully')
      resolve()
    }
    script.onerror = (error) => {
      console.error('Failed to load Google Maps API:', error)
      reject(new Error('Failed to load Google Maps API'))
    }
    
    document.head.appendChild(script)
  })
}

// Initialize the map
const initializeMap = async () => {
  try {
    isLoading.value = true
    error.value = null

    await loadGoogleMapsAPI()
    
    // Wait for the DOM to be ready and the container to be available
    await nextTick()
    
    // Try multiple times to find the container
    let attempts = 0
    const maxAttempts = 10
    
    while (!mapContainer.value && attempts < maxAttempts) {
      await new Promise(resolve => setTimeout(resolve, 100))
      attempts++
    }

    if (!mapContainer.value) {
      console.error('Map container not found after', maxAttempts, 'attempts')
      error.value = 'Map container not found'
      isLoading.value = false
      return
    }
    
    // Initialize geocoder
    geocoder.value = new google.maps.Geocoder()

    // Geocode the address to get coordinates
    geocoder.value.geocode({ address: props.address }, (results, status) => {      
      if (status === 'OK' && results[0]) {
        const location = results[0].geometry.location
        console.log('Location found:', location.lat(), location.lng())

        // Create map
        map.value = new google.maps.Map(mapContainer.value, {
          center: location,
          zoom: props.zoom,
          mapTypeId: props.mapTypeId,
          styles: [
            {
              featureType: 'poi',
              elementType: 'labels',
              stylers: [{ visibility: 'off' }]
            }
          ]
        })

        // Create marker
        marker.value = new google.maps.Marker({
          position: location,
          map: map.value,
          title: props.address,
          animation: google.maps.Animation.DROP
        })

        // Add info window
        const infoWindow = new google.maps.InfoWindow({
          content: `<div class="map__info"><strong>${props.address}</strong></div>`
        })

        marker.value.addListener('click', () => {
          infoWindow.open(map.value, marker.value)
        })

        console.log('Map initialized successfully')
        isLoading.value = false
      } else {
        console.error('Geocoding failed:', status)
        error.value = `Geocoding failed: ${status}`
        isLoading.value = false
      }
    })
  } catch (err) {
    console.error('Map initialization error:', err)
    error.value = err.message
    isLoading.value = false
  }
}

// Update map when address changes
const updateMapLocation = () => {
  if (!geocoder.value || !map.value) return

  geocoder.value.geocode({ address: props.address }, (results, status) => {
    if (status === 'OK' && results[0]) {
      const location = results[0].geometry.location
      
      map.value.setCenter(location)
      map.value.setZoom(props.zoom)
      
      if (marker.value) {
        marker.value.setPosition(location)
        marker.value.setTitle(props.address)
      }
    }
  })
}

// Watch for prop changes
watch(() => props.address, updateMapLocation)
watch(() => props.zoom, (newZoom) => {
  if (map.value) {
    map.value.setZoom(newZoom)
  }
})

onMounted(() => {
  initializeMap()
})
</script>

<template>
  <div
    class="map-header"
    v-if="header">
    <h2 id="accommodations">{{ header }}</h2>
  </div>
  <div class="map">
    <div class="map__content">
      <h3>{{ heading }}</h3>
      <h4>{{ subheading }}</h4>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Explicabo facilis, repellat reprehenderit cumque fugit voluptates deserunt nihil nesciunt sed.</p>
    </div>
    <div class="map__container">
      <div 
        ref="mapContainer"
        class="map__element"
        v-show="!isLoading && !error"
      ></div>
      
      <div 
        v-if="isLoading" 
        class="map__loading"
      >
        <div class="map__loading-spinner"></div>
        <p>Loading map...</p>
      </div>
      
      <div 
        v-if="error" 
        class="map__error"
      >
        <p>Error: {{ error }}</p>
      </div>
    </div>
  </div>
</template>
