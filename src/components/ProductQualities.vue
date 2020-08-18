<template>
  <div>
    <h3>Banana qualities</h3>
    <div v-for="quality in qualities" :key="quality.id">
      <p>{{ quality.name }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";

interface ProductQualitiesInterface {
  id: number;
  name: string;
  quantity: number;
}

@Component
export default class ProductQualities extends Vue {
  @Prop() qualities: ProductQualitiesInterface[];
}
</script>
