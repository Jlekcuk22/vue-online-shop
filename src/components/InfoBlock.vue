<script setup>
defineProps({
  title: String,
  description: String,
  imageUrl: String,
});
</script>

<template>
  <div class="flex flex-col items-center text-center mx-auto w-72">
    <img class="w-24 h-24" :src="imageUrl" alt="Info image" />
    <h2 class="text-2xl font-bold mb-2 mt-5">{{ title }}</h2>
    <p class="text-gray-400 text-base">{{ description }}</p>
  </div>
</template>

<style scoped></style>
