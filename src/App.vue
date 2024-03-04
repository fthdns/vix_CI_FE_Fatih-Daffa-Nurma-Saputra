<template>
  <div id="app">
    <ProductDisplay :product="product" :category="category" />
    <button @click="getNextProduct">Next Product</button>
  </div>
</template>

<script>
import ProductDisplay from "./components/ProductDisplay.vue";

export default {
  name: "App",
  components: {
    ProductDisplay,
  },
  data() {
    return {
      product: null,
      category: null,
      index: 1,
    };
  },
  methods: {
    async getNextProduct() {
      this.index = this.index >= 20 ? 1 : this.index + 1;
      await this.fetchProduct();
    },
    async fetchProduct() {
      try {
        const response = await fetch(`https://fakestoreapi.com/products/${this.index}`);
        const data = await response.json();
        if (data.category === "men's clothing" || data.category === "women's clothing") {
          this.product = data;
          this.category = data.category;
        } else {
          this.product = null;
          this.category = null;
        }
      } catch (error) {
        console.error(error);
      }
    },
  },
  mounted() {
    this.fetchProduct();
  },
};
</script>

<style lang="css" src="./assets/style/page.css"></style>

