<template>
  <div>
    <h1>{{ title }}</h1>
    <a :href="link">macacos me mordam</a>
    <br />
    <span v-if="onSale"
      >You can shop bananas right here, press the link 🆙</span
    >
    <span v-else :class="{ 'out-of-stock': !onSale }"
      >Out of stock of 🍌🍌🍌</span
    >
    <ProductQualities :qualities="qualities" />
    <p>Bananas ({{ cart }})</p>
    <button v-on:click="addToCart" :disabled="!onSale">
      Add bananas to cart
    </button>
    <button v-if="cart > 0" v-on:click="removeFromCart">
      Remove bananas from cart
    </button>
  </div>
</template>

<script lang="ts">
import ProductQualities from "./ProductQualities.vue";
import { Component, Prop, Vue } from "vue-property-decorator";
@Component({
  components: { ProductQualities }
})
export default class Product extends Vue {
  @Prop({ default: "Banana product component" }) product!: string;
  @Prop({ default: "Joel" }) productOwner!: string;

  // define a reactive property on a vue component
  // https://michaelnthiessen.com/property-or-method-not-defined/
  data() {
    return {
      link: "http://www.staggeringbeauty.com/",
      selectedQuality: 0,
      qualities: [
        { id: 1, name: "madeira", quantity: 3 },
        { id: 2, name: "porto santo", quantity: 4 },
        { id: 3, name: "continente", quantity: 5 }
      ],
      cart: 0
    };
  }

  addToCart() {
    this.cart += 1;
  }

  removeFromCart() {
    this.cart -= 1;
  }

  updateProduct(index) {
    this.selectedQuality = index;
  }

  get title() {
    return (
      "praise for ♥️ " +
      this.productOwner +
      " - " +
      this.product +
      " king 🍌🍌🍌"
    );
  }

  get onSale() {
    return this.qualities[this.selectedQuality].quantity > 0;
  }
}
</script>
