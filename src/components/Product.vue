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
    <button v-on:click="addToCart" :disabled="!onSale">
      Add bananas to cart
    </button>
    <button v-on:click="removeFromCart">remove bananas from cart</button>

    <div>
      <h3>Reviews</h3>
      <p v-if="!reviews.length">There's no reviews</p>
      <ul>
        <li v-for="review in reviews" :key="review.name">
          <p>{{ review.name }}</p>
          <p>{{ review.review }}</p>
        </li>
      </ul>
    </div>
    <ProductReview @review-submitted="addReview" />
  </div>
</template>

<script lang="ts">
import ProductQualities from "./ProductQualities.vue";
import ProductReview from "./ProductReview.vue";
import { Component, Prop, Vue } from "vue-property-decorator";
@Component({
  components: { ProductQualities, ProductReview }
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
      reviews: []
    };
  }

  addToCart() {
    this.$emit("add-to-cart", this.qualities[this.selectedQuality].id);
  }

  removeFromCart() {
    this.$emit("remove-from-cart", this.qualities[this.selectedQuality].id);
  }

  addReview(productReview) {
    this.reviews.push(productReview);
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
