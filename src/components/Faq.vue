<script setup>
import IconLeaf from '../components/IconLeaf.vue'

defineProps({
  question: {
    type: String,
    required: true,
  },
  answer: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <details class="faq__item">
    <summary class="faq__question">
      <IconLeaf />
      {{ question }}
    </summary>
    <div class="faq__answer">
      {{ answer }}
    </div>
  </details>
</template>
