<template>
  <div class="product-grid-item">
    <img class="product-image" :src="product.image" />
    <p class="product-name">{{ product.brand }}</p>
  </div>
</template>

<script>
export default {
  name: 'ProductGridItem',
  props: {
    product: { type: Object, required: true, default: () => ({}) },
  },
};
</script>

<style scoped>
.product-grid-item {
  display: flex;
  flex-wrap: wrap;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.3);
  width: 60%;
  height: auto;
  align-items: center;
}

.product-image {
  width: 10%;
}
</style>
