<script setup>
import { RouterLink, RouterView, useRoute } from 'vue-router'
import { ref, watch, onMounted } from 'vue'

const route = useRoute()
const transitionName = ref('fade')

// Watch route changes to determine transition direction
watch(
  () => route.fullPath,
  (to, from) => {
    // Use simple fade transition for all route changes
    transitionName.value = 'fade'
    
    // Immediately scroll to top when route changes (no animation)
    window.scrollTo(0, 0)
  }
)

function setVh() {
  const vh = window.innerHeight * 0.01;
  document.documentElement.style.setProperty('--vh', `${vh}px`);
}


onMounted(() => {
  setVh();
  // window.addEventListener('resize', setVh);
});
</script>

<template>
  <header>
    <!-- <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" /> -->

    <div class="header">
      <nav class="header__nav">
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/colors">Colors</RouterLink>
      </nav>
    </div>
  </header>

  <Transition :name="transitionName" mode="out-in">
    <RouterView :key="$route.fullPath" />
  </Transition>
</template>

<style>
/* Simple fade transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

<!-- <style scoped>
  
</style> -->
