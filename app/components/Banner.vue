<template>
    <div class="w-full mx-auto px-2">
  <div class=" bg-white dark:bg-gray-800 rounded-lg shadow-lg overflow-hidden">
    <!-- Banner Container -->
    <div 
      class="relative h-64 md:h-80 cursor-pointer"
      @touchstart="handleTouchStart"
      @touchend="handleTouchEnd"
      @click="goToLink"
    >
      <!-- Background Image -->
      <div class="absolute inset-0">
        <img 
          :src="currentBanner.image" 
          :alt="currentBanner.title"
          class="w-full h-full object-cover"
        />
        <div class="absolute inset-0 bg-black/50 bg-opacity-20 dark:bg-opacity-40"></div>
      </div>

      <!-- Content Overlay -->
      <div class="relative z-10 h-full flex items-center justify-center text-center p-6">
        <div class="text-white">
          <h2 class="text-2xl md:text-4xl font-bold mb-2">{{ currentBanner.title }}</h2>
          <p class="text-lg md:text-xl opacity-90">{{ currentBanner.subtitle }}</p>
        </div>
      </div>



      <!-- Dots Navigation -->
      <div v-if="banners.length > 1" class="absolute bottom-4 left-1/2 -translate-x-1/2 flex space-x-2">
        <button 
          v-for="(banner, index) in banners" 
          :key="index"
          @click.stop="currentSlide = index"
          :class="[
            'w-2 h-2 rounded-full transition-all duration-200',
            currentSlide === index 
              ? 'bg-white w-8' 
              : 'bg-white bg-opacity-50 hover:bg-opacity-75'
          ]"
        ></button>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import { ref, computed, onMounted, onUnmounted } from 'vue'

export default {
  name: 'NikeDunkBanner',
  setup() {
    const currentSlide = ref(0)
    const touchStart = ref(0)
    const touchEnd = ref(0)
    let autoSlideInterval = null

    // Banner data - rasm va link
    const banners = ref([
      {
        id: 1,
        title: "Nike Dunk Low Panda",
        subtitle: "Classic Black & White",
        image: "https://images.unsplash.com/photo-1549298916-b41d501d3772?w=800&h=400&fit=crop",
        link: "https://nike.com/dunk-low-panda"
      },
      {
        id: 2,
        title: "Nike Dunk High Chicago",
        subtitle: "Legendary Red & White",
        image: "https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=800&h=400&fit=crop",
        link: "https://nike.com/dunk-high-chicago"
      },
      {
        id: 3,
        title: "Nike Dunk Low Syracuse",
        subtitle: "Bold Orange Design",
        image: "https://images.unsplash.com/photo-1606107557195-0e29a4b5b4aa?w=800&h=400&fit=crop",
        link: "https://nike.com/dunk-low-syracuse"
      }
    ])

    const currentBanner = computed(() => banners.value[currentSlide.value])

    const nextSlide = () => {
      currentSlide.value = (currentSlide.value + 1) % banners.value.length
    }

    const previousSlide = () => {
      currentSlide.value = currentSlide.value === 0 ? banners.value.length - 1 : currentSlide.value - 1
    }

    const handleTouchStart = (e) => {
      touchStart.value = e.targetTouches[0].clientX
    }

    const handleTouchEnd = (e) => {
      touchEnd.value = e.changedTouches[0].clientX
      handleSwipeGesture()
    }

    const handleSwipeGesture = () => {
      if (!touchStart.value || !touchEnd.value) return
      
      const distance = touchStart.value - touchEnd.value
      const isLeftSwipe = distance > 50
      const isRightSwipe = distance < -50

      if (isLeftSwipe) {
        nextSlide()
      }
      if (isRightSwipe) {
        previousSlide()
      }
    }

    const goToLink = () => {
      window.open(currentBanner.value.link, '_blank')
    }

    const startAutoSlide = () => {
      autoSlideInterval = setInterval(() => {
        nextSlide()
      }, 6000) // 3 soniyada auto slide
    }

    const stopAutoSlide = () => {
      if (autoSlideInterval) {
        clearInterval(autoSlideInterval)
        autoSlideInterval = null
      }
    }

    onMounted(() => {
      startAutoSlide()
    })

    onUnmounted(() => {
      stopAutoSlide()
    })

    return {
      currentSlide,
      banners,
      currentBanner,
      nextSlide,
      previousSlide,
      handleTouchStart,
      handleTouchEnd,
      goToLink
    }
  }
}
</script>