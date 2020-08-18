<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>show me {{ product }} 🍌🍌🍌</h1>
    <a :href="link">macacos me mordam</a>
    <br />
    <span v-if="onSale"
      >You can shop bananas right here, press the link 🆙</span
    >
    <h3>Banana qualities</h3>
    <div v-for="quality in qualities" :key="quality.id">
      <p>{{ quality.name }}</p>
    </div>
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import HelloWorld from "./components/HelloWorld.vue";

@Component({
  components: {
    HelloWorld
  }
})
export default class App extends Vue {
  // define a reactive property on a vue component
  // https://michaelnthiessen.com/property-or-method-not-defined/
  data() {
    return {
      product: "bananas",
      link: "http://www.staggeringbeauty.com/",
      onSale: true,
      qualities: [
        { id: 1, name: "madeira" },
        { id: 2, name: "porto santo" },
        { id: 3, name: "continente" }
      ]
    };
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
</style>
