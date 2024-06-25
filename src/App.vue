<template>
  <button @click="changePage" class="btn-switcher">
    <template v-if="selectedPage === 'ProductsPage'"> Enable Vue Query </template>
    <template v-else> Disable Vue Query </template>
  </button>
  <ProductsPage v-if="selectedPage === 'ProductsPage'" />
  <OptimisedProductsPage v-else />
</template>

<script setup>
import ProductsPage from "./pages/ProductsPage.vue";
import OptimisedProductsPage from "./pages/OptimisedProductsPage.vue";

import { ref } from "vue";

const selectedPage = ref("ProductsPage");

function changePage() {
  selectedPage.value =
    selectedPage.value === "ProductsPage" ? "OptimisedProductsPage" : "ProductsPage";
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.btn-switcher {
  background-color: #009879;
  color: #ffffff;
  border: 1px solid #dddddd;
  padding: 12px 15px;
  font-weight: bold;
  margin: 0 auto;
  display: block;
  cursor: pointer;
  border: 1px solid #13aa52;
  border-radius: 4px;
  box-shadow: rgba(0, 0, 0, 0.1) 0 2px 4px 0;

  transform: translateY(0);
  transition: transform 150ms, box-shadow 150ms;
  &:hover {
    box-shadow: rgba(0, 0, 0, 0.15) 0 3px 9px 0;
    transform: translateY(-2px);
  }
}
</style>
