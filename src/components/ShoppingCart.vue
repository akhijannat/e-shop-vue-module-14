<script setup>
import { computed, ref } from "vue";
import { useStore } from "vuex";

const store = useStore();
const cart = computed(() => store.state.cart);
const cartTotal = computed(() => {
  return cart.value.reduce(
    (total, item) => total + item.price * item.quantity,
    0
  );
});

function removeFromCart(productId) {
  store.commit("removeFromCart", productId);
}
</script>

<template>
  <div>
    <h2>Shopping Cart</h2>
    <ul>
      <li v-for="item in cart" :key="item.id">
        {{ item.name }} - {{ item.quantity }} - ${{ item.price }}
        <button @click="removeFromCart(item.id)">Remove</button>
      </li>
    </ul>
    <p>Total: ${{ cartTotal }}</p>
  </div>
</template>
