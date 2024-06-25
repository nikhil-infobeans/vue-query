<script setup>
import { ref } from "vue";
import BoringTable from "@/components/BoringTable.vue";
import ProductModal from "@/components/ProductModal.vue";

const data = ref();
const loading = ref(false);

async function fetchData() {
  loading.value = true;
  const response = await fetch(
    `https://dummyjson.com/products?limit=10`
  ).then((res) => res.json());
  data.value = response.products;
  loading.value = false;
}

fetchData();

const selectedProduct = ref();
function onSelect(item) {
  selectedProduct.value = item;
}
</script>

<template>
  <div class="container">
    <ProductModal
      v-if="selectedProduct"
      :product-id="selectedProduct.id"
      @close="selectedProduct = null"
    />
    <BoringTable :items="data" v-if="!loading" @select="onSelect" />
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
