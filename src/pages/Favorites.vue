<script setup>
import axios from "axios";
import { onMounted, ref } from "vue";
import CardList from "../components/CardList.vue";

const favorites = ref([]);

onMounted(async () => {
  try {
    const { data } = await axios.get(
      "https://f39c66e620e8f05c.mokky.dev/favorites?_relations=items",
    );
    favorites.value = data.map((obj) => obj.item);
  } catch (e) {
    console.log(e);
  }
});
</script>

<template>
  <h1 class="text-3xl font-bold mb-8">Мои закладки</h1>
  <CardList :items="favorites" is-favorites />
</template>

<style scoped></style>
