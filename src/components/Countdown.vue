<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  // target date/time in ISO format
  targetDate: {
    type: String, // e.g. '2025-07-01T12:00:00Z'
    required: true,
  },
})

const hours = ref('00')
const minutes = ref('00')
const seconds = ref('00')
const days = ref('00')

let intervalId = null

const updateTimer = () => {
  const now = new Date().getTime()
  const target = new Date('2026-10-31T16:00:00Z').getTime()
  const diff = target - now

  if (diff <= 0) {
    clearInterval(intervalId)
    days.value = hours.value = minutes.value = seconds.value = '00'
    return
  }

  const totalSeconds = Math.floor(diff / 1000)
  const d = Math.floor(totalSeconds / (3600 * 24))
  const h = Math.floor((totalSeconds % (3600 * 24)) / 3600)
  const m = Math.floor((totalSeconds % 3600) / 60)
  const s = totalSeconds % 60

  days.value = String(d).padStart(2, '0')
  hours.value = String(h).padStart(2, '0')
  minutes.value = String(m).padStart(2, '0')
  seconds.value = String(s).padStart(2, '0')
}

onMounted(() => {
  updateTimer()
  intervalId = setInterval(updateTimer, 1000)
})

onUnmounted(() => {
  clearInterval(intervalId)
})
</script>

<template>
  <div class="countdown">
    <div class="countdown__container">
      <div class="countdown__timer">
        <span class="countdown__timer-wrapper">
          <span class="countdown__timer-time">{{ days }}</span>
          <span class="countdown__timer-text">days</span>
        </span>
        <span class="countdown__timer-wrapper">
          <span class="countdown__timer-time">{{ hours }}</span>
          <span class="countdown__timer-text">hours</span>
        </span>
        <span class="countdown__timer-wrapper">
          <span class="countdown__timer-time">{{ minutes }}</span>
          <span class="countdown__timer-text">minutes</span>
        </span>
        <span class="countdown__timer-wrapper">
          <span class="countdown__timer-time">{{ seconds }}</span>
          <span class="countdown__timer-text">seconds</span>
        </span>
      </div>
    </div>
  </div> 
</template>