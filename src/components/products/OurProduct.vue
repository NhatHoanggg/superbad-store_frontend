<script setup>
import { ref, onBeforeMount } from 'vue'
import { getOurProductsApi } from '@/services/product.service'
import ProductItem from './ProductItem.vue'

const products = ref([
  {
    id: '3608dd0d-1a91-4583-8f01-c0af6048bb4e',
    name: 'Product 1aaa generally warm mark hurry did teach who especially sugar tears sentence progress table hollow sharp done thumb better chance planned business due beautiful graph',
    minPrice: 100,
    maxPrice: 150,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.5,
    sold: 100,
  },
  {
    id: '4608dd0d-1a91-4583-8f01-c0af6048bb4f',
    name: 'Product 2',
    minPrice: 200,
    maxPrice: 250,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.2,
    sold: 85,
  },
  {
    id: '5608dd0d-1a91-4583-8f01-c0af6048bb50',
    name: 'Product 3',
    minPrice: 150,
    maxPrice: 180,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.7,
    sold: 120,
  },
  {
    id: '6608dd0d-1a91-4583-8f01-c0af6048bb51',
    name: 'Product 4',
    minPrice: 300,
    maxPrice: 350,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.0,
    sold: 65,
  },
  {
    id: '7608dd0d-1a91-4583-8f01-c0af6048bb52',
    name: 'Product 5',
    minPrice: 180,
    maxPrice: 220,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.8,
    sold: 150,
  },
  {
    id: '8608dd0d-1a91-4583-8f01-c0af6048bb53',
    name: 'Product 6',
    minPrice: 250,
    maxPrice: 280,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.3,
    sold: 95,
  },
  {
    id: '9608dd0d-1a91-4583-8f01-c0af6048bb54',
    name: 'Product 7',
    minPrice: 120,
    maxPrice: 160,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.6,
    sold: 110,
  },
  {
    id: 'a608dd0d-1a91-4583-8f01-c0af6048bb55',
    name: 'Product 8',
    minPrice: 350,
    maxPrice: 400,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.1,
    sold: 75,
  },
  {
    id: 'b608dd0d-1a91-4583-8f01-c0af6048bb56',
    name: 'Product 9',
    minPrice: 220,
    maxPrice: 260,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.4,
    sold: 88,
  },
  {
    id: 'c608dd0d-1a91-4583-8f01-c0af6048bb57',
    name: 'Product 10',
    minPrice: 280,
    maxPrice: 320,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.9,
    sold: 180,
  },
  {
    id: 'd608dd0d-1a91-4583-8f01-c0af6048bb58',
    name: 'Product 11',
    minPrice: 160,
    maxPrice: 190,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.2,
    sold: 70,
  },
  {
    id: 'e608dd0d-1a91-4583-8f01-c0af6048bb59',
    name: 'Product 12',
    minPrice: 400,
    maxPrice: 450,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.7,
    sold: 130,
  },
  {
    id: 'f608dd0d-1a91-4583-8f01-c0af6048bb60',
    name: 'Product 13',
    minPrice: 190,
    maxPrice: 230,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.5,
    sold: 105,
  },
  {
    id: 'g608dd0d-1a91-4583-8f01-c0af6048bb61',
    name: 'Product 14',
    minPrice: 320,
    maxPrice: 360,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.3,
    sold: 90,
  },
  {
    id: 'h608dd0d-1a91-4583-8f01-c0af6048bb62',
    name: 'Product 15',
    minPrice: 240,
    maxPrice: 270,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.8,
    sold: 160,
  },
  {
    id: 'i608dd0d-1a91-4583-8f01-c0af6048bb63',
    name: 'Product 16',
    minPrice: 270,
    maxPrice: 300,
    imageUrl: 'https://via.placeholder.com/150',
    rating: 4.6,
    sold: 140,
  },
])

const visibleProducts = ref(8)
const showMore = () => {
  visibleProducts.value += 8
}

const showLess = () => {
  visibleProducts.value = 8
}

onBeforeMount(async () => {
  try {
    const res = await getOurProductsApi()
    products.value = res.data.data
    console.log(res.data)
  } catch (error) {
    console.log(error)
  }
})
</script>

<template>
  <div class="w-full h-fit bg-[#f9f9f9] rounded-md">
    <!-- title section -->
    <div class="w-full flex justify-between p-4">
      <div class="flex">
        <h2 class="text-xl font-bold">Recommend For You</h2>
      </div>
    </div>

    <!-- products grid -->
    <div class="w-full p-4">
      <div class="grid grid-cols-4 gap-4">
        <RouterLink
          v-for="product in products.slice(0, visibleProducts)"
          :key="product.id"
          :to="`/products/${product.id}`"
          class="w-full"
        >
          <ProductItem :product="product" />
        </RouterLink>
      </div>

      <!-- Action buttons -->
      <div class="w-full flex justify-center gap-4 mt-6">
        <button
          v-if="visibleProducts < products.length"
          @click="showMore"
          class="flex items-center gap-2 px-6 py-2 bg-primary-600 text-black rounded-full shadow-md hover:bg-primary-700 transition-all duration-300 hover:scale-105"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            stroke-width="2"
          >
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 4v16m8-8H4" />
          </svg>
          <span>See more</span>
        </button>

        <button
          v-if="visibleProducts > 8"
          @click="showLess"
          class="flex items-center gap-2 px-6 py-2 bg-gray-200 text-gray-700 rounded-full shadow-md hover:bg-gray-300 transition-all duration-300 hover:scale-105"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            stroke-width="2"
          >
            <path stroke-linecap="round" stroke-linejoin="round" d="M20 12H4" />
          </svg>
          <span>See less</span>
        </button>
      </div>
    </div>
  </div>
</template>
