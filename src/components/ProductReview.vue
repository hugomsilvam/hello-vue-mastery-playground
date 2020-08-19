<template>
  <div>
    <p>Did you like the product? 💪</p>
    <form @submit.prevent="onSubmit">
      <div v-if="errors.length">
        <p>Please fill the fields to review 🍌🍌🍌🍌</p>
        <ul>
          <li v-for="error in errors" :key="error">{{ error }}</li>
        </ul>
      </div>

      <input type="text" v-model="name" placeholder="your name" />
      <br />
      <input
        type="radio"
        id="yes"
        v-model="review"
        name="product-review"
        value="yes"
      />
      <label for="male">Yes</label>
      <br />
      <input
        type="radio"
        id="no"
        v-model="review"
        name="product-review"
        value="no"
      />
      <label for="female">No</label>
      <br />
      <input
        type="radio"
        id="other"
        v-model="review"
        name="product-review"
        value="other"
      />
      <label for="other">Dont know</label>
      <input type="submit" value="submit" />
    </form>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
@Component
export default class ProductReview extends Vue {
  data() {
    return {
      name: null,
      review: null,
      errors: []
    };
  }

  onSubmit() {
    if (this.name && this.review) {
      const productReview = {
        name: this.name,
        review: this.review
      };

      this.$emit("review-submitted", productReview);

      // clean state
      this.name = null;
      this.review = null;
      this.errors = [];
    } else {
      if (!this.name) {
        this.errors.push("Required name 🥳");
      }
      if (!this.review) {
        this.errors.push("Required review value 💩");
      }
    }
  }
}
</script>
