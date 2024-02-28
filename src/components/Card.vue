<script setup>
const props = defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickFavorite: Function,
  onClickAdd: Function,
});

const visibleFavoriteBtn = Boolean(props.onClickAdd);
</script>

<template>
  <div
    class="relative bg-white border border-slate-100 rounded-3xl p-2 md:p-4 lg:p-8 cursor-pointer transition duration-500 hover:-translate-y-2 hover:shadow-xl"
  >
    <div class="flex flex-col justify-between h-full">
      <div>
        <img
          v-if="visibleFavoriteBtn"
          @click="onClickFavorite"
          :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
          alt="like 1"
          class="absolute top-4 lg:top-8 left-4 lg:left-8"
        />
        <img class="w-full h-36" :src="imageUrl" alt="snicker" />
        <p class="mt-3">{{ title }}</p>
      </div>
      <div class="flex justify-between mt-5">
        <div class="flex flex-col">
          <span class="text-slate-400">Цена:</span>
          <b>{{ price }}</b>
        </div>
        <img
          v-if="onClickFavorite"
          @click="onClickAdd"
          :src="!isAdded ? '/plus.svg' : '/checked.svg'"
          alt="Plus"
        />
      </div>
    </div>
  </div>
</template>

<style scoped></style>
