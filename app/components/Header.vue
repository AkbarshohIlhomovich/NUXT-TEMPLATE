<template>
  <div>
    <!-- Header -->
    <header class="relative z-50">
      <div class="px-2 py-3 flex items-center justify-between w-full">
        <!-- Hamburger Menu -->
        <button 
          @click="isDrawerOpen = !isDrawerOpen"
          class="py-2 hover:bg-gray-700 dark:hover:bg-gray-600 rounded-lg transition-colors duration-200"
        >
          <div class="w-6 h-6 flex flex-col justify-center items-center">
            <div 
              class="w-5 h-0.5 bg-white mb-1 transition-all duration-300"
              :class="isDrawerOpen ? 'rotate-45 translate-y-1.5 mb-0' : ''"
            ></div>
            <div 
              class="w-5 h-0.5 bg-white mb-1 transition-all duration-300"
              :class="isDrawerOpen ? 'opacity-0' : ''"
            ></div>
            <div 
              class="w-5 h-0.5 bg-white transition-all duration-300"
              :class="isDrawerOpen ? '-rotate-45 -translate-y-1.5' : ''"
            ></div>
          </div>
        </button>

        <!-- Logo -->
        <h1 v-if="!isSearchActive" class="text-xl font-bold text-white text-nowrap">CASUAL store</h1>

        <!-- Search -->
        <div class="flex items-center">
          <div class="search-container" :class="{ 'search-active': isSearchActive }">
            <UInput
              v-show="isSearchActive"
              v-model="searchQuery"
              variant="soft"
              ref="searchInput"
              type="text"
              size="lg"
              rounded="full"
              placeholder="Qidirish..."
              class="search-input rounded-full"
            />
          </div>
          <UButton 
            variant="ghost"
            @click="toggleSearch"
            class="p-2 rounded-lg transition-colors ml-2 text-white"
          >
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path 
                v-if="!isSearchActive"
                stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
              />
              <path 
                v-else
                stroke-linecap="round" stroke-linejoin="round" stroke-width="2" 
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
          </UButton>
        </div>
      </div>
    </header>

    <!-- Overlay -->
    <transition name="overlay">
      <div 
        v-if="isDrawerOpen"
        @click="isDrawerOpen = false"
        class="fixed inset-0 bg-black bg-opacity-50 z-40"
      ></div>
    </transition>

    <!-- Drawer -->
    <transition name="drawer">
      <div 
        v-if="isDrawerOpen"
        class="fixed left-0 top-0 h-full w-80 bg-white dark:bg-[#17212B] shadow-lg z-50 overflow-y-auto"
      >
      <div class="p-4">
        
        <!-- Menu Links -->
        <nav class="space-y-2">
          <a 
            v-for="link in menuLinks" 
            :key="link.text"
            :href="link.href"
            @click="isDrawerOpen = false"
            class="block py-3 text-gray-700 dark:text-gray-300 rounded-lg transition-all duration-200 hover:translate-x-1 font-medium"
          >
            {{ link.text }}
          </a>
        </nav>


        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import { ref, nextTick } from 'vue'

export default {
  setup() {
    const isDrawerOpen = ref(false)
    const isSearchActive = ref(false)
    const searchQuery = ref('')
    const searchInput = ref(null)

    const menuLinks = [
      { text: 'O nas', href: '/about' },
      { text: 'Otzyvy o nas', href: '/reviews' },
      { text: 'Garantiya', href: '/warranty' },
      { text: 'Kak oplatit "DOLYAMI"?', href: '/payment' },
      { text: 'O vozvrate', href: '/returns' },
      { text: 'O dostavke', href: '/delivery' },
      { text: 'Nash telegram kanal', href: '/telegram' }
    ]

    const toggleSearch = async () => {
      if (isSearchActive.value) {
        isSearchActive.value = false
        searchQuery.value = ''
      } else {
        isSearchActive.value = true
        await nextTick()
        searchInput.value?.focus()
      }
    }

    const handleSearchBlur = () => {
      if (!searchQuery.value.trim()) {
        setTimeout(() => isSearchActive.value = false, 200)
      }
    }

    return {
      isDrawerOpen,
      isSearchActive,
      searchQuery,
      searchInput,
      menuLinks,
      toggleSearch,
      handleSearchBlur
    }
  }
}
</script>

<style scoped>
/* Overlay animatsiya */
.overlay-enter-active,
.overlay-leave-active {
  transition: opacity 0.3s ease;
}

.overlay-enter-from,
.overlay-leave-to {
  opacity: 0;
}

/* Drawer animatsiya */
.drawer-enter-active,
.drawer-leave-active {
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.drawer-enter-from,
.drawer-leave-to {
  transform: translateX(-100%);
}

.search-container {
  width: 0;
  overflow: hidden;
  transition: width 0.3s ease;
}

.search-container.search-active {
  width: 250px;
}

.search-input {
  width: 250px;
  transition: opacity 0.2s ease 0.1s;
}

.search-container:not(.search-active) .search-input {
  opacity: 0;
}

@media (max-width: 640px) {
  .search-container.search-active {
    width: 200px;
  }
  .search-input {
    width: 200px;
  }
}
</style>