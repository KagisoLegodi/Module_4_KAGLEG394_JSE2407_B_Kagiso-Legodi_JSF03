<template>
    <div class="sort">
      <select @change="handleSortChange" v-model="sortOrder">
        <option value="">Default</option>
        <option value="low-to-high">Price: Low to High</option>
        <option value="high-to-low">Price: High to Low</option>
      </select>
    </div>
  </template>
  