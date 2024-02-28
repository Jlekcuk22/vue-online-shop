<script setup>
import { ref, provide, watch, computed } from "vue";

import Header from "./components/Header.vue";
import Sidebar from "./components/Sidebar.vue";
import axios from "axios";

/* Корзина (START) */
const cart = ref([]);

const sidebarOpen = ref(false);

const totalPrice = computed(() =>
  cart.value.reduce((acc, item) => acc + item.price, 0),
);
const vatPrice = computed(() => Math.round((totalPrice.value * 5) / 100));

const closeSidebar = () => {
  sidebarOpen.value = false;
};

const openSidebar = () => {
  sidebarOpen.value = true;
};

const addToCart = (item) => {
  cart.value.push(item);
  item.isAdded = true;
};

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1);
  item.isAdded = false;
};

watch(
  cart,
  () => {
    localStorage.setItem("cart", JSON.stringify(cart.value));
  },
  { deep: true },
);

provide("cart", {
  cart,
  closeSidebar,
  openSidebar,
  addToCart,
  removeFromCart,
});

/* Корзина (END) */
</script>

<template>
  <Sidebar v-if="sidebarOpen" :total-price="totalPrice" :vat-price="vatPrice" />
  <div class="bg-white w-4/5 m-auto h-full rounded-xl shadow-xl mt-20">
    <Header :total-price="totalPrice" @open-sidebar="openSidebar" />

    <div class="p-8">
      <router-view></router-view>
    </div>
  </div>
</template>

<style scoped></style>
