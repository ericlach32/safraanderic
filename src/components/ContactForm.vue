<script setup>
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
</script>

<template>
  <form
    action="https://getform.io/f/bvrmmoob"
    method="POST"
    id="contact-form"
    class="form">

    <div class="form__header">
      <h2>Contact Us</h2>
    </div>

    <div class="form__wrapper">

      <div class="input-wrapper">
        <label for="firstName" class="visually-hidden">First Name</label>
        <input
          type="text"
          name="firstName"
          id="firstName"
          autocomplete="off"
          placeholder="First Name"
          class="input">
      </div>

      <div class="input-wrapper">
        <label for="lastName" class="visually-hidden">Last Name</label>
        <input
          type="text"
          name="lastName"
          id="lastName"
          autocomplete="off"
          placeholder="Last Name"
          class="input">
      </div>

      <div class="input-wrapper">
        <label for="message" class="visually-hidden">Message</label>
        <textarea
          rows="5"
          name="message"
          id="message"
          autocomplete="off"
          placeholder="Message"
          class="input"></textarea>
      </div>

      <div class="input-wrapper">
        <button
          type="submit"
          class="btn btn-1 hover-filled-opacity">
          <span>Submit</span>
        </button>
      </div>

    </div>
  </form>
</template>