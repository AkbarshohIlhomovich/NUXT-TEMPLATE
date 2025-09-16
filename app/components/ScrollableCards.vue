<template>
  <div class="w-full">
    <!-- Horizontal Scroll Container -->
    <div class="flex space-x-4 p-2 overflow-x-scroll">
      <!-- Card Items -->
      <a 
        v-for="card in cards" 
        :key="card.id"
        :href="card.link"
        class="flex-shrink-0 w-32 h-32 rounded-2xl overflow-hidden shadow-lg hover:shadow-xl transition-shadow duration-300"
      >
        <img 
          :src="card.image" 
          :alt="card.alt"
          class="w-full h-full object-cover hover:scale-105 transition-transform duration-300"
        />
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HorizontalScrollCards',
  data() {
    return {
      cards: [
        {
          id: 1,
          image: "https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=300&h=300&fit=crop",
          alt: "Watch",
          link: "/watch"
        },
        {
          id: 2,
          image: "https://images.unsplash.com/photo-1553062407-98eeb64c6a62?w=300&h=300&fit=crop",
          alt: "Bag",
          link: "/bag"
        },
        {
          id: 3,
          image: "https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=300&h=300&fit=crop",
          alt: "Store",
          link: "/store"
        },
        {
          id: 4,
          image: "https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?w=300&h=300&fit=crop",
          alt: "Phone",
          link: "/phone"
        },
        {
          id: 5,
          image: "https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?w=300&h=300&fit=crop",
          alt: "Food",
          link: "/food"
        },
        {
          id: 6,
          image: "https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=300&h=300&fit=crop",
          alt: "Headphones",
          link: "/headphones"
        },
        {
          id: 7,
          image: "https://images.unsplash.com/photo-1542291026-7eec264c27ff?w=300&h=300&fit=crop",
          alt: "Shoes",
          link: "/shoes"
        },
        {
          id: 8,
          image: "https://images.unsplash.com/photo-1526170375885-4d8ecf77b99f?w=300&h=300&fit=crop",
          alt: "Camera",
          link: "/camera"
        }
      ]
    }
  }
}
</script>