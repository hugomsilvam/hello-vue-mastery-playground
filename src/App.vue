<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
    <Product @add-to-cart="addToCart" @remove-from-cart="removeFromCart" />
    <p>Cart ({{ cart.length }})</p>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "./components/HelloWorld.vue";
import Product from "./components/Product.vue";

@Component({
  components: {
    HelloWorld,
    Product
  }
})
export default class App extends Vue {
  data() {
    return {
      cart: []
    };
  }

  addToCart(productID) {
    this.cart.push(productID);
  }

  removeFromCart(productID) {
    for (let i = 0; i < this.cart.length; i++) {
      if (this.cart[i] === productID) {
        this.cart.splice(i, 1);
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.out-of-stock {
  text-decoration: line-through;
}
</style>
