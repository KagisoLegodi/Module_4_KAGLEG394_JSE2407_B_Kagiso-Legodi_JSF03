<template>
  <div>
    <div class="container mx-auto p-4">
      <!-- Header -->
      <h1 class="text-2xl font-bold mb-4 text-center">Vue E-store</h1>

      <!-- Filters Section -->
      <div class="filters">
        <Filter
          :categories="categories"
          :initialCategory="selectedCategory"
          @update:category="handleCategoryChange"
        />
        <Sort :initialSort="sortOrder" @update:sort="handleSortChange" />
      </div>

      <!-- Loading State -->
      <div v-if="loading">
        <ProductSkeleton v-for="n in 3" :key="n" />
      </div>

      <!-- Product List -->
      <div v-else class="product-list">
        <div
          v-for="product in filteredProducts"
          :key="product.id"
          class="product-card"
        >
          <router-link
            :to="{ path: `/product/${product.id}`, query: $route.query }"
          >
            <img
              :src="product.image"
              :alt="product.title"
              class="product-image"
            />
            <h3 class="title">{{ product.title }}</h3>
            <p class="price">${{ product.price }}</p>
            <p>{{ product.category }}</p>
            <p>Ratings: {{ product.rating.rate }}</p>
            <p>Reviews: {{ product.rating.count }}</p>
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, watch, computed } from "vue";
import { useRoute, useRouter } from "vue-router";
import ProductSkeleton from "./ProductSkeleton.vue";
import Filter from "./Filter.vue";
import Sort from "./Sort.vue";
import { filterProducts, fetchCategories } from "../productUtils";

export default {
  name: "ProductList",
  components: {
    ProductSkeleton,
    Filter,
    Sort,
  },
  setup() {
    const route = useRoute();
    const router = useRouter();

    const loading = ref(true);
    const products = ref([]);
    const categories = ref([]);
    const selectedCategory = ref(route.query.category || "");
    const sortOrder = ref(route.query.sort || "");

    const filteredProducts = computed(() => {
      return filterProducts(
        products.value,
        selectedCategory.value,
        sortOrder.value
      );
    });

    const fetchProducts = async () => {
      try {
        await new Promise((resolve) => setTimeout(resolve, 2000));
        const response = await fetch("https://fakestoreapi.com/products");
        const data = await response.json();
        products.value = data;
      } catch (error) {
        console.error(error);
      } finally {
        loading.value = false;
      }
    };

    const fetchCategoriesData = async () => {
      categories.value = await fetchCategories();
    };

    return {
      route,
      router,
      loading,
      products,
      categories,
      selectedCategory,
      sortOrder,
      filteredProducts,
      fetchProducts,
      fetchCategoriesData,
    };
  },
};
</script>
