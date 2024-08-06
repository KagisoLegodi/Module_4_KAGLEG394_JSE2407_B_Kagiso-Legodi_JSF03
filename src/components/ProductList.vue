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
          <div v-for="product in filteredProducts" :key="product.id" class="product-card">
            <router-link :to="{ path: `/product/${product.id}`, query: $route.query }">
              <img :src="product.image" :alt="product.title" class="product-image" />
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
  