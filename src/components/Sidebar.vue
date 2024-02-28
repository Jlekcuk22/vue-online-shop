<script setup>
import SidebarHead from "./SidebarHead.vue";
import CartItemList from "./CartItemList.vue";
import InfoBlock from "./InfoBlock.vue";
import axios from "axios";
import { computed, inject, ref } from "vue";

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number,
  buttonDisabled: Boolean,
});

const isCreating = ref(false);
const orderId = ref(null);

const { cart, closeSidebar } = inject("cart");

const createOrder = async () => {
  try {
    isCreating.value = true;
    const { data } = await axios.post(
      "https://f39c66e620e8f05c.mokky.dev/orders",
      {
        items: cart.value,
        totalPrice: props.totalPrice.value,
      },
    );

    cart.value = [];

    orderId.value = data.id;
  } catch (e) {
    console.log(e);
  } finally {
    isCreating.value = false;
  }
};

const cartIsEmpty = computed(() => cart.value.length === 0);

const buttonDisabled = computed(() => isCreating.value || cartIsEmpty.value);
</script>

<template>
  <div
    class="fixed top-0 left-0 h-screen w-full bg-black z-10 opacity-75"
  ></div>
  <div class="bg-white w-96 h-full fixed right-0 top-0 z-20 p-8 flex flex-col">
    <SidebarHead />

    <div v-if="!totalPrice || orderId" class="h-full flex items-center">
      <InfoBlock
        v-if="!totalPrice && !orderId"
        title="Корзина пустая"
        description="Добавьте хотя бы одну пару кроссовок, чтобы сделать заказ."
        image-url="/package-icon.png"
      />
      <InfoBlock
        v-if="orderId"
        title="Заказ оформлен!"
        :description="`Ваш заказ #${orderId} скоро будет передан курьерской доставке`"
        image-url="/order-success-icon.png"
      />
    </div>
    <div v-else>
      <CartItemList />

      <div class="flex flex-col gap-3 mt-7">
        <div class="flex gap-2">
          <span>Итого</span>
          <div
            class="flex-1 border-b border-dotted border-slate-300 mb-1.5"
          ></div>
          <b>{{ totalPrice }} лей</b>
        </div>
        <div class="flex gap-2">
          <span>Налог 5%</span>
          <div
            class="flex-1 border-b border-dotted border-slate-300 mb-1.5"
          ></div>
          <b>{{ vatPrice }} лей</b>
        </div>
        <button
          :disabled="buttonDisabled"
          @click="createOrder"
          class="mt-4 bg-lime-500 w-full rounded-xl py-3 text-white hover:bg-lime-600 transition duration-500 active:bg-lime-700 disabled:bg-slate-400 cursor-pointer"
        >
          Оформить заказ
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
