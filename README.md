# Vue E-store

## Introduction
Welcome to the Vue E-store! This project is a web application designed to showcase products in a user-friendly manner. It features a detailed view modal to display comprehensive product information, including images, ratings, descriptions, and options to add items to the cart (not yet functional).

## Technologies Used
- **HTML/CSS**: For structuring and styling the components.
- **Vue.js**: For handling state and interactivity in a lightweight manner.
- **Tailwind CSS**: For utility-first CSS styling.
- **JavaScript**: For additional functionality and dynamic content handling.

## Setup Instructions
To get started with this project, follow these steps:

1. **Clone the Repository**
   ```bash
   git clone https://github.com/KagisoLegodi/Module_2_KAGLEG394_JSE2407-B_KagisoLegodi_JSF01.git
   ```

2. **Navigate to the Project Directory**
   ```bash
   cd alpine-final
   ```

3. **Install Dependencies**
   Ensure you have Node.js and npm installed, then run:
   ```bash
   npm install
   ```

4. **Run the Development Server**
   Start the development server to view the application locally:
   ```bash
   npm start
   ```
   Open your browser and navigate to [http://localhost:3000](http://localhost:3000) to see the application in action.

## Usage Examples

### Detailed View Page
The detailed view modal component displays detailed information about a selected product. It features:
- **Product Image**: Displayed on the left side of the modal.
- **Product Title**: Shown prominently at the top.
- **Rating**: Includes a star rating and the number of reviews, if available.
- **Description**: A brief overview of the product.
- **Action Buttons**: Go back to the home page.

Here's the Vue.js structure for the Details page:

```vue
<template>
  <div class="product-detail">
    <img :src="product.image" :alt="product.title" class="product-image" />
    <h1>{{ product.title }}</h1>
    <p class="price">${{ product.price }}</p>
    <p>Category: {{ product.category }}</p>
    <p>Ratings: {{ product.rating.rate }} (Based on {{ product.rating.count }} reviews)</p>
    <p>{{ product.description }}</p>
    <router-link to="/" class="back-button">Back to Products</router-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: null,
      productId: this.$route.params.id || ''
    }
  },
  mounted() {
    this.fetchProduct()
  },
  methods: {
    async fetchProduct() {
      try {
        const res = await fetch(`https://fakestoreapi.com/products/${this.productId}`)
        if (res.ok) {
          this.product = await res.json()
        } else {
          console.error('Failed to fetch product')
        }
      } catch (error) {
        console.error('Error fetching product:', error)
      }
    }
  }
}
</script>

<style>
  .product-detail {
    max-width: 100%;
    margin: 0 auto;
    text-align: center;
    font-weight: bold;
    padding: 1.5rem;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .product-detail img {
    max-width: 30%;
  }
  h1 {
    font-size: 2rem;
    margin-bottom: 0.5rem;
    color: #333;
  }
  p {
    font-size: 1rem;
    margin: 0.5rem 0;
    color: #555;
  }
  .price {
    font-weight: bold;
    color: #1a202c;
  }
  @media (max-width: 600px) {
    .product-detail {
      width: 100%;
    }
  }
</style>
```

## Contributing
We welcome contributions to improve the project. Please follow these guidelines:
1. **Fork the Repository**
2. **Create a Feature Branch**
3. **Commit Your Changes**
4. **Push to the Branch**
5. **Create a Pull Request**

## License
This project is licensed under the MIT License - see the LICENSE file for details.