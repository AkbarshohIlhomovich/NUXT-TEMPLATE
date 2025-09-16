<template>
  <div>
    <div class="px-2">
      <!-- Categories Scroll -->
      <div class="flex overflow-x-auto space-x-1 pb-2 scrollbar-hide">
        <!-- Sort Drawer -->
        <UDrawer v-model="showSortDrawer" :overlay="true">
          <button
            class="flex-shrink-0 flex items-center space-x-2 px-2 py-1.5 bg-white dark:bg-gray-800 rounded-full border border-gray-200 dark:border-gray-700 shadow-sm hover:shadow-md transition-all duration-200"
            :class="{ 'bg-blue-50 dark:bg-blue-900 border-blue-200 dark:border-blue-700': selectedSort }"
          >
            <UIcon name="i-heroicons-bars-arrow-up" class="w-4 h-4 text-gray-600 dark:text-gray-400" />
            <span v-if="selectedSort" class="text-sm font-medium text-gray-700 dark:text-gray-300">
              {{ selectedSort || '' }}
            </span>
          </button>

          <template #content>
            <div class="p-6">              
              <h3 class="text-xl font-bold text-gray-800 dark:text-white mb-6">Saralash</h3>
              
              <div class="space-y-3">
                <div
                  v-for="sort in sortOptions"
                  :key="sort.value"
                  @click="selectSort(sort)"
                  class="flex items-center justify-between p-4 rounded-lg border border-gray-200 dark:border-gray-700 cursor-pointer hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors"
                  :class="{ 'bg-blue-50 dark:bg-blue-900 border-blue-200 dark:border-blue-700': selectedSort === sort.label }"
                >
                  <div>
                    <p class="font-medium text-gray-800 dark:text-white">{{ sort.label }}</p>
                    <p class="text-sm text-gray-500 dark:text-gray-400">{{ sort.description }}</p>
                  </div>
                  <UIcon 
                    v-if="selectedSort === sort.label" 
                    name="i-heroicons-check-circle" 
                    class="w-5 h-5 text-blue-500" 
                  />
                </div>
              </div>
            </div>
          </template>
        </UDrawer>

        <!-- Categories Drawer -->
        <UDrawer v-model="showCategoriesDrawer" :overlay="true">
          <button
            class="flex-shrink-0 flex items-center space-x-2 px-2 py-1.5 bg-white dark:bg-gray-800 rounded-full border border-gray-200 dark:border-gray-700 shadow-sm hover:shadow-md transition-all duration-200"
            :class="{ 'bg-blue-50 dark:bg-blue-900 border-blue-200 dark:border-blue-700': selectedCategory }"
          >
            <UIcon name="i-heroicons-squares-2x2" class="w-4 h-4 text-gray-600 dark:text-gray-400" />
            <span class="text-sm font-medium text-gray-700 dark:text-gray-300">
              {{ selectedCategory || 'Kategoriyalar' }}
            </span>
          </button>

          <template #content>
            <div class="p-6">              
              <h3 class="text-xl font-bold text-gray-800 dark:text-white mb-6">Kategoriyalar</h3>
              
              <div class="grid grid-cols-2 gap-3 overflow-y-auto">
                <div
                  v-for="category in allCategories"
                  :key="category.id"
                  @click="selectCategory(category)"
                  class="flex flex-col p-4 rounded-lg border border-gray-200 dark:border-gray-700 cursor-pointer hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors"
                  :class="{ 'bg-blue-50 dark:bg-blue-900 border-blue-200 dark:border-blue-700': selectedCategory === category.name }"
                >
                  <span class="font-medium text-gray-800 dark:text-white mb-1">{{ category.name }}</span>
                  <span class="text-xs text-gray-500 dark:text-gray-400">{{ category.count }} mahsulot</span>
                </div>
              </div>
            </div>
          </template>
        </UDrawer>

        <!-- Category Items -->
        <div
          v-for="category in displayCategories"
          :key="category.id"
          @click="selectCategory(category)"
          class="flex-shrink-0 flex items-center space-x-2 px-2 py-1.5 bg-white dark:bg-gray-800 rounded-full border border-gray-200 dark:border-gray-700 shadow-sm hover:shadow-md transition-all duration-200 cursor-pointer"
          :class="{ 'bg-blue-500 text-white border-blue-500': selectedCategory === category.name }"
        >
          <span class="text-sm font-medium">{{ category.name }}</span>
          <UBadge 
            v-if="category.count" 
            :label="category.count.toString()"
            size="xs" 
            variant="soft"
            :class="selectedCategory === category.name ? 'bg-blue-400 text-white' : ''"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const showSortDrawer = ref(false)
const showCategoriesDrawer = ref(false)
const selectedSort = ref('')
const selectedCategory = ref('')

const sortOptions = [
  { value: 'popular', label: 'Mashhur', description: 'Eng ko\'p sotilgan mahsulotlar' },
  { value: 'newest', label: 'Yangi', description: 'Eng yangi mahsulotlar' },
  { value: 'price_low', label: 'Arzon', description: 'Narx bo\'yicha o\'sish' },
  { value: 'price_high', label: 'Qimmat', description: 'Narx bo\'yicha kamayish' },
  { value: 'rating', label: 'Reyting', description: 'Eng yuqori baholangan' },
  { value: 'discount', label: 'Chegirma', description: 'Eng katta chegirmalar' }
]

const allCategories = [
  { id: 1, name: 'Elektronika', count: 1250 },
  { id: 2, name: 'Kiyim', count: 890 },
  { id: 3, name: 'Uy jihozlari', count: 654 },
  { id: 4, name: 'Sport', count: 432 },
  { id: 5, name: 'Kitoblar', count: 321 },
  { id: 6, name: 'Go\'zallik', count: 567 },
  { id: 7, name: 'Avtomobil', count: 234 },
  { id: 8, name: 'Bolalar', count: 445 },
  { id: 9, name: 'Oziq-ovqat', count: 678 },
  { id: 10, name: 'Mebel', count: 156 },
  { id: 11, name: 'Texnika', count: 789 },
  { id: 12, name: 'Telefon', count: 1100 }
]

const displayCategories = computed(() => allCategories.slice(0, 6))

const selectSort = (sort) => {
  selectedSort.value = sort.label
  showSortDrawer.value = false
}

const selectCategory = (category) => {
  selectedCategory.value = category.name
  showCategoriesDrawer.value = false
}
</script>

<style scoped>
.scrollbar-hide {
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.scrollbar-hide::-webkit-scrollbar {
  display: none;
}
</style>