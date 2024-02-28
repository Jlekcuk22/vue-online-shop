<script setup>
defineProps({
  totalPrice: Number,
});

const emit = defineEmits(["openSidebar"]);
</script>

<template>
  <header
    class="flex flex-column justify-between items-center border-b border-slate-200 px-10 py-8"
  >
    <router-link to="/">
      <div class="flex items-center gap-4">
        <img src="/logo.png" alt="Logo" class="w-10" />
        <div class="">
          <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
          <p class="text-slate-400 text-sm">Магазин лучших кроссовок</p>
        </div>
      </div>
    </router-link>
    <div>
      <ul class="flex items-center md:gap-4 lg:gap-10">
        <li
          @click="() => emit('openSidebar')"
          class="flex items-center gap-1.5 lg:gap-3 text-gray-500 hover:text-black cursor-pointer"
        >
          <img src="/cart.svg" alt="Cart" />
          <b class="hidden md:block">{{ totalPrice }} лей</b>
        </li>
        <router-link to="/favorites">
          <li
            class="flex items-center gap-1.5 lg:gap-3 text-gray-500 hover:text-black cursor-pointer"
          >
            <img src="/heart.svg" alt="Heart" />
            <span class="hidden md:block">Закладки</span>
          </li>
        </router-link>
        <li
          class="flex items-center gap-1.5 lg:gap-3 text-gray-500 hover:text-black cursor-pointer"
        >
          <img src="/profile.svg" alt="Profile" />
          <span class="hidden md:block">Профиль</span>
        </li>
      </ul>
    </div>
  </header>
</template>

<style scoped></style>
