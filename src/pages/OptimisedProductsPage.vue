<script setup>
import { ref } from "vue";
import { useQuery } from "vue-query";

import BoringTable from "@/components/BoringTable.vue";
import OptimisedProductModal from "@/components/OptimisedProductModal.vue";

async function fetchData() {
  return await fetch(`https://dummyjson.com/products?limit=10`).then((res) => res.json());
}

const { isLoading, data } = useQuery(
  "products",
  fetchData
);

const selectedProduct = ref();
function onSelect(item) {
  selectedProduct.value = item;
}
</script>

<template>
  <div class="container">
    <OptimisedProductModal
      v-if="selectedProduct"
      :product-id="selectedProduct.id"
      @close="selectedProduct = null"
    />
    <BoringTable :items="data.products" v-if="!isLoading" @select="onSelect" />
  </div>
</template>

<style scoped lang="scss">
.container {
  max-width: 960px;
  margin-right: auto;
  margin-left: auto;
  display: flex;
  justify-content: center;
  flex-direction: column;
}
</style>
