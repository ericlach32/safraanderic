<script setup>
import { onMounted, onUnmounted, ref, watch, nextTick } from 'vue'

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
  copy: {
    type: String
  },
  address: {
    type: String,
    required: true,
    default: 'New York, NY'
  },
  name: {
    type: String,
    default: ''
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
const infoWindow = ref(null)
const isLoading = ref(true)
const error = ref(null)

// Generate unique ID for this map instance
const mapId = ref('map-' + Math.random().toString(36).substr(2, 9))

// Global API loading state to prevent multiple script loads
let apiLoadingPromise = null

// Load Google Maps API (singleton pattern to prevent multiple loads)
const loadGoogleMapsAPI = () => {
  // If API is already loaded, resolve immediately
  if (window.google && window.google.maps) {
    return Promise.resolve()
  }

  // If API is currently loading, return the existing promise
  if (apiLoadingPromise) {
    return apiLoadingPromise
  }

  // Create new loading promise
  apiLoadingPromise = new Promise((resolve, reject) => {
    const script = document.createElement('script')
    script.src = 'https://maps.googleapis.com/maps/api/js?key=' + props.apiKey + '&libraries=places'
    script.async = true
    script.defer = true
    
    script.onload = () => {
      console.log('Google Maps API loaded successfully')
      resolve()
    }
    script.onerror = (error) => {
      console.error('Failed to load Google Maps API:', error)
      apiLoadingPromise = null // Reset so we can try again
      reject(new Error('Failed to load Google Maps API'))
    }
    
    document.head.appendChild(script)
  })

  return apiLoadingPromise
}

// Initialize the map
const initializeMap = async () => {
  try {
    isLoading.value = true
    error.value = null

    await loadGoogleMapsAPI()
    
    // Wait for the DOM to be ready and the container to be available
    await nextTick()
    
    // Try multiple times to find the container, with increasing delays
    let attempts = 0
    const maxAttempts = 20
    
    while (!mapContainer.value && attempts < maxAttempts) {
      // Use exponential backoff for better reliability
      const delay = Math.min(50 * Math.pow(1.5, attempts), 500)
      await new Promise(resolve => setTimeout(resolve, delay))
      attempts++
      
      // Additional check: try to find container by ID if ref is not working
      if (!mapContainer.value && attempts > 5) {
        const containerElement = document.getElementById(mapId.value)
        if (containerElement) {
          mapContainer.value = containerElement
          console.log('Found container by ID for ' + mapId.value)
          break
        }
      }
    }

    if (!mapContainer.value) {
      console.error('Map container not found for ' + mapId.value + ' after', maxAttempts, 'attempts')
      error.value = 'Map container not found'
      isLoading.value = false
      return
    }

    // Ensure the container is visible and has dimensions
    const rect = mapContainer.value.getBoundingClientRect()
    if (rect.width === 0 || rect.height === 0) {
      console.warn('Map container ' + mapId.value + ' has no dimensions, waiting...')
      await new Promise(resolve => setTimeout(resolve, 100))
    }

    console.log('Initializing map ' + mapId.value + ' for address: ' + props.address)
    
    // Initialize geocoder
    geocoder.value = new google.maps.Geocoder()

    // Geocode the address to get coordinates
    geocoder.value.geocode({ address: props.address }, (results, status) => {      
      if (status === 'OK' && results[0]) {
        const location = results[0].geometry.location
        
        // Validate coordinates before using them
        const lat = location.lat()
        const lng = location.lng()
        
        if (!isFinite(lat) || !isFinite(lng) || isNaN(lat) || isNaN(lng)) {
          console.error('Invalid coordinates received:', lat, lng)
          error.value = 'Invalid coordinates received from geocoding service'
          isLoading.value = false
          return
        }
        
        console.log('Location found:', lat, lng)

        // Create map with validated coordinates
        map.value = new google.maps.Map(mapContainer.value, {
          center: { lat: lat, lng: lng },
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

        // Create marker with validated coordinates
        marker.value = new google.maps.Marker({
          position: { lat: lat, lng: lng },
          map: map.value,
          title: props.name || props.address,
          animation: google.maps.Animation.DROP
        })

        // Create info window content
        const infoWindowContent = 
          '<div class="map__info">' +
            '<div class="map__info-header">' +
              '<h4 class="map__info-title">' + (props.name || 'Location') + '</h4>' +
            '</div>' +
            '<div class="map__info-body">' +
              '<p class="map__info-address">' + props.address + '</p>' +
              '<a href="https://www.google.com/maps/dir/?api=1&destination=' + encodeURIComponent(props.address) + '" ' +
                 'target="_blank" ' +
                 'class="btn btn--small">' +
                '<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">' +
                  '<path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>' +
                  '<circle cx="12" cy="10" r="3"></circle>' +
                '</svg>' +
                'Get Directions' +
              '</a>' +
            '</div>' +
          '</div>'

        // Create unique info window for this map instance
        infoWindow.value = new google.maps.InfoWindow({
          content: infoWindowContent
        })

        marker.value.addListener('click', () => {
          infoWindow.value.open(map.value, marker.value)
        })

        console.log('Map ' + mapId.value + ' initialized successfully')
        isLoading.value = false
      } else {
        console.error('Geocoding failed:', status)
        
        // Provide more specific error messages based on status
        let errorMessage = 'Geocoding failed: ' + status
        if (status === 'ZERO_RESULTS') {
          errorMessage = 'Address not found: ' + props.address
        } else if (status === 'OVER_QUERY_LIMIT') {
          errorMessage = 'Geocoding service quota exceeded'
        } else if (status === 'REQUEST_DENIED') {
          errorMessage = 'Geocoding request denied - check API key'
        } else if (status === 'INVALID_REQUEST') {
          errorMessage = 'Invalid geocoding request'
        }
        
        error.value = errorMessage
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
      
      // Validate coordinates before using them
      const lat = location.lat()
      const lng = location.lng()
      
      if (!isFinite(lat) || !isFinite(lng) || isNaN(lat) || isNaN(lng)) {
        console.error('Invalid coordinates received in updateMapLocation:', lat, lng)
        return
      }
      
      map.value.setCenter({ lat: lat, lng: lng })
      map.value.setZoom(props.zoom)
      
      if (marker.value) {
        marker.value.setPosition({ lat: lat, lng: lng })
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

// Cleanup function
const cleanup = () => {
  if (marker.value) {
    marker.value.setMap(null)
    marker.value = null
  }
  if (infoWindow.value) {
    infoWindow.value.close()
    infoWindow.value = null
  }
  if (map.value) {
    map.value = null
  }
  if (geocoder.value) {
    geocoder.value = null
  }
  console.log('Cleaned up map ' + mapId.value)
}

onMounted(async () => {
  // Add a small random delay to prevent race conditions when multiple maps mount simultaneously
  const delay = Math.random() * 200 // 0-200ms random delay
  await new Promise(resolve => setTimeout(resolve, delay))
  
  console.log('Mounting map ' + mapId.value)
  initializeMap()
})

onUnmounted(() => {
  cleanup()
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
      <div v-html="copy"></div>
    </div>
    <div class="map__container">
      <div 
        ref="mapContainer"
        :id="mapId"
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