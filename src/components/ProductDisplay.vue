<template>
  <div :class="productClass">
    <div v-if="product" class="product-info">
      <h2>{{ product.title }}</h2>
      <p>{{ product.description }}</p>
      <p>{{ product.price }}</p>
    </div>
    <div v-else>
      <p>This product is unavailable to show</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductDisplay",
  props: {
    product: Object,
    category: String,
  },
  computed: {
    productClass() {
      return {
        "men-section": this.category === "men's clothing",
        "women-section": this.category === "women's clothing",
        "unavailable-product": !this.product,
      };
    },
  },
};
</script>

<style lang="css">
/* Add your styles for men-section, women-section, and unavailable-product here */
</style>
