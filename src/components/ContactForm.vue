<script setup>
import { ref, reactive } from 'vue'

const props = defineProps({
  heading: {
    type: String,
    required: true,
  },
  subheading: {
    type: String,
    required: true,
  },
})

// Form state
const isSubmitting = ref(false)
const submitStatus = ref('') // 'success', 'error', or ''
const formData = reactive({
  firstName: '',
  lastName: '',
  message: ''
})

// Form submission handler
const handleSubmit = async (event) => {
  event.preventDefault()
  
  if (isSubmitting.value) return
  
  isSubmitting.value = true
  submitStatus.value = ''
  
  try {
    const response = await fetch('https://getform.io/f/bvrmmoob', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(formData)
    })
    
    if (response.ok) {
      submitStatus.value = 'success'
      // Reset form
      formData.firstName = ''
      formData.lastName = ''
      formData.message = ''
    } else {
      throw new Error('Submission failed')
    }
  } catch (error) {
    console.error('Form submission error:', error)
    submitStatus.value = 'error'
  } finally {
    isSubmitting.value = false
  }
}

// Clear status message after 5 seconds
const clearStatus = () => {
  setTimeout(() => {
    submitStatus.value = ''
  }, 5000)
}

// Watch for status changes to auto-clear
import { watch } from 'vue'
watch(submitStatus, (newStatus) => {
  if (newStatus) {
    clearStatus()
  }
})
</script>

<template>
  <form
    @submit="handleSubmit"
    id="contact-form"
    class="form">

    <div class="form__header">
      <h2>Contact Us</h2>
    </div>

    <div v-if="submitStatus === 'success'" class="form__status form__status--success">
      <p>Thank you! Your message has been sent successfully.</p>
    </div>
    
    <div v-if="submitStatus === 'error'" class="form__status form__status--error">
      <p>Sorry, there was an error sending your message. Please try again.</p>
    </div>

    <div class="form__wrapper">

      <div class="input-wrapper">
        <label for="firstName" class="visually-hidden">First Name</label>
        <input
          v-model="formData.firstName"
          type="text"
          name="firstName"
          id="firstName"
          autocomplete="off"
          placeholder="First Name"
          class="input"
          required>
      </div>

      <div class="input-wrapper">
        <label for="lastName" class="visually-hidden">Last Name</label>
        <input
          v-model="formData.lastName"
          type="text"
          name="lastName"
          id="lastName"
          autocomplete="off"
          placeholder="Last Name"
          class="input"
          required>
      </div>

      <div class="input-wrapper">
        <label for="message" class="visually-hidden">Message</label>
        <textarea
          v-model="formData.message"
          rows="5"
          name="message"
          id="message"
          autocomplete="off"
          placeholder="Message"
          class="input"
          required></textarea>
      </div>

      <div class="input-wrapper">
        <button
          type="submit"
          :disabled="isSubmitting"
          class="btn btn-1 hover-filled-opacity">
          <span v-if="!isSubmitting">Submit</span>
          <span v-else>Sending...</span>
        </button>
      </div>

    </div>
  </form>
</template>