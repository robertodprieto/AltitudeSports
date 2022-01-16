<template>
  <div class="layout-row wrap justify-content-center">
    <section
      v-for="(product, index) in products"
      :key="index"
      :data-testid="'product-item-' + index"
      class="w-30 product-item"
    >
      <div class="card ma-16">
        <img :src="product.image" class="product-image" :alt="product.name" />
        <div class="card-text pa-4">
          <h5 class="ma-0 text-center">{{ product.name }}</h5>
          <p class="ma-0 mt-8 text-center">${{ product.price }}</p>
        </div>
        <div class="card-actions justify-content-center pa-4">
          <button
            class="x-small outlined"
            data-testid="btn-item-add"
            v-if="checkProductInCart(product)"
            @click="addToCart(product)"
          >
            Add To Cart
          </button>

          <button
            class="x-small danger"
            data-testid="btn-item-remove"
            v-if="!checkProductInCart(product)"
            @click="removeFromCart(product)"
          >
            Remove
          </button>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "ProductList",
  props: {
    products: Array,
    cart: Object,
  },
  methods: {
    addToCart(product) {
      this.$emit("add-to-cart", product);
    },
    removeFromCart(product) {
      this.$emit("remove-from-cart", product);
    },
    checkProductInCart(product) {
      return this.cart.items.filter((item) => item.id === product.id).length ===
        0
        ? true
        : false;
    },
  },
};
</script>

<style scoped lang="scss">
.product-image {
  margin: 32px 30%;
  width: 40%;
  min-height: 90px;
}
</style>
