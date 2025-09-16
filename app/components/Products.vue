<template>
  <div class="w-full bg-gray-100 dark:bg-gray-900 p-2">
    <!-- Product Grid -->
    <div class="grid grid-cols-2 gap-4">
      <!-- Product Card -->
      <div 
        v-for="product in products" 
        :key="product.id"
        class="bg-white dark:bg-gray-800 rounded-2xl shadow-lg overflow-hidden hover:shadow-xl transition-shadow duration-300"
      >
        <!-- Image Carousel -->
        <div 
          class="relative h-48 bg-gray-200 dark:bg-gray-700"
          @touchstart="handleTouchStart($event, product.id)"
          @touchend="handleTouchEnd($event, product.id)"
        >
          <!-- Main Image -->
          <img 
            :src="product.images[currentImageIndex[product.id] || 0]" 
            :alt="product.name"
            class="w-full h-full object-cover"
          />
          
          <!-- Image Navigation Dots -->
          <div 
            v-if="product.images.length > 1" 
            class="absolute bottom-2 left-1/2 -translate-x-1/2 flex space-x-1"
          >
            <button 
              v-for="(image, index) in product.images" 
              :key="index"
              @click="setCurrentImage(product.id, index)"
              :class="[
                'w-2 h-2 rounded-full transition-all duration-200',
                (currentImageIndex[product.id] || 0) === index 
                  ? 'bg-white w-4' 
                  : 'bg-white/50'
              ]"
            ></button>
          </div>

          <!-- Image Counter -->
          <div 
            v-if="product.images.length > 1"
            class="absolute top-2 right-2 bg-black/50 text-white text-xs px-2 py-1 rounded-full"
          >
            {{ (currentImageIndex[product.id] || 0) + 1 }}/{{ product.images.length }}
          </div>
        </div>

        <!-- Product Info -->
        <div class="p-4">
          <!-- Price -->
          <div class="flex items-center space-x-2 mb-2">
            <span class="text-base font-bold text-gray-900 dark:text-white">
              {{ product.price }} ₽
            </span>
            <span 
              v-if="product.originalPrice" 
              class="text-xs text-gray-500 dark:text-gray-400 line-through"
            >
              {{ product.originalPrice }} ₽
            </span>
          </div>

          <!-- Product Name -->
          <h3 class="text-gray-800 dark:text-gray-200 font-medium text-xs leading-tight">
            {{ product.name }}
          </h3>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductGrid',
  data() {
    return {
      currentImageIndex: {}, // Track current image for each product
      touchStart: {},
      products: [
        {
          id: 1,
          name: 'Adidas Samba "Wonder White Maroon"',
          price: '11 747',
          originalPrice: '15 760',
          images: [
            'https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1606107557195-0e29a4b5b4aa?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1549298916-b41d501d3772?w=400&h=300&fit=crop'
          ]
        },
        {
          id: 2,
          name: 'Adidas "Samba OG Black"',
          price: '9 650',
          originalPrice: '11 650',
          images: [
            'https://images.unsplash.com/photo-1595950653106-6c9ebd614d3a?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1508378388172-bfa8b008c5e5?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1551107696-a4b0c5a0d9a2?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1460353581641-37baddab0fa2?w=400&h=300&fit=crop'
          ]
        },
        {
          id: 3,
          name: 'Kappa "Tiro"',
          price: '7 750',
          images: [
            'https://images.unsplash.com/photo-1600185365483-26d7a4cc7519?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?w=400&h=300&fit=crop'
          ]
        },
        {
          id: 4,
          name: 'Adidas Samba "Lucid Pink"',
          price: '9 750',
          originalPrice: '12 750',
          images: [
            'https://images.unsplash.com/photo-1607522370275-f14206abe5d3?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1594219890896-74dd46511c5b?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1584464491033-06628f3a6b7b?w=400&h=300&fit=crop'
          ]
        },
        {
          id: 5,
          name: 'Nike Air Force 1 "White"',
          price: '8 990',
          images: [
            'https://images.unsplash.com/photo-1549298916-b41d501d3772?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1580902394724-b08ff9ba7e8a?w=400&h=300&fit=crop'
          ]
        },
        {
          id: 6,
          name: 'Converse Chuck Taylor All Star',
          price: '5 490',
          originalPrice: '6 990',
          images: [
            'https://images.unsplash.com/photo-1606107557195-0e29a4b5b4aa?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1551107696-a4b0c5a0d9a2?w=400&h=300&fit=crop',
            'https://images.unsplash.com/photo-1562183241-b937e95585b6?w=400&h=300&fit=crop'
          ]
        }
      ]
    }
  },
  methods: {
    setCurrentImage(productId, imageIndex) {
      this.currentImageIndex = {
        ...this.currentImageIndex,
        [productId]: imageIndex
      }
    },
    handleTouchStart(e, productId) {
      this.touchStart[productId] = e.touches[0].clientX
    },
    handleTouchEnd(e, productId) {
      if (!this.touchStart[productId]) return
      
      const touchEnd = e.changedTouches[0].clientX
      const touchDistance = this.touchStart[productId] - touchEnd
      const minSwipeDistance = 50
      
      if (Math.abs(touchDistance) > minSwipeDistance) {
        const currentIndex = this.currentImageIndex[productId] || 0
        const maxIndex = this.products.find(p => p.id === productId).images.length - 1
        
        if (touchDistance > 0) {
          // Swipe left - next image
          const newIndex = currentIndex < maxIndex ? currentIndex + 1 : 0
          this.setCurrentImage(productId, newIndex)
        } else {
          // Swipe right - previous image
          const newIndex = currentIndex > 0 ? currentIndex - 1 : maxIndex
          this.setCurrentImage(productId, newIndex)
        }
      }
      
      delete this.touchStart[productId]
    }
  }
}
</script>