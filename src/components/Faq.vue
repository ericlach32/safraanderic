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
      <span>{{ question }}</span>
    </summary>
    <div class="faq__answer" v-html="answer"></div>
  </details>
</template>
