<script setup>
import { RouterLink, RouterView, useRoute } from 'vue-router'
import { ref, watch, onMounted } from 'vue'

const route = useRoute()
const transitionName = ref('slide-left')

// Watch route changes to determine transition direction
watch(
  () => route.fullPath,
  (to, from) => {
    const routesOrder = ['/', '/about', '/colors']
    const toIndex = routesOrder.indexOf(to)
    const fromIndex = routesOrder.indexOf(from)
    transitionName.value = toIndex < fromIndex ? 'slide-right' : 'slide-left'
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
/* Shared base styles for all transitions */
.slide-left-enter-active,
.slide-left-leave-active,
.slide-right-enter-active,
.slide-right-leave-active {
  position: absolute;
  width: 100%;
  top: 0;
  left: 0;
}

/* Incoming page (fade in only) */
.slide-left-enter-active,
.slide-right-enter-active {
  opacity: 0;
  animation: fadeIn 0.6s ease forwards;
}

/* Outgoing page (slide out) */
.slide-left-leave-active {
  animation: slideOutLeft 0.6s ease forwards;
}
.slide-right-leave-active {
  animation: slideOutRight 0.6s ease forwards;
}

/* Keyframes */
@keyframes slideOutLeft {
  from {
    transform: translateX(0%);
    opacity: 1;
  }
  to {
    transform: translateX(-50%);
    opacity: 0;
  }
}

@keyframes slideOutRight {
  from {
    transform: translateX(0%);
    opacity: 1;
  }
  to {
    transform: translateX(50%);
    opacity: 0;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: scale(0.98);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}
</style>

<!-- <style scoped>
  
</style> -->
