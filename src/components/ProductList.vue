<script setup>
import { RouterLink, RouterView } from "vue-router";

import Hero from "./Hero.vue";
import WhyShopWithUs from "./WhyShopWithUs.vue";
import NewArrivals from "./NewArrivals.vue";

import axios from "axios";
import { ref, onBeforeMount } from "vue";
const products = ref([]);

onBeforeMount(() => {
  axios.get("https://dummyjson.com/products").then((res) => {
    products.value = res.data.products;
  });
});

const detailsBtn =
  "text-center font-semibold transition duration-200 rounded py-1 px-3 text-white bg-gray-600 hover:scale-105";
</script>
<template>
  <Hero />

  <WhyShopWithUs />
  <NewArrivals />

  <section class="container mx-auto py-20 px-10">
    <h1 class="text-2xl md:text-5xl font-serif font-semibold pb-2 text-center">
      Featured Products
    </h1>
    <p class="text-center">
      Lorem ipsum dolor sit amet, consectetur adipiscing elit.
    </p>

    <div class="h-1 bg-gray-600 w-52 mx-auto my-3"></div>
    <div class="grid grid-cols-1 md:grid-cols-5 gap-7 mt-5 md:mt-10">
      <div
        class="shadow hover:shadow-lg cursor-pointer"
        v-for="product in products"
        :key="product.id"
      >
        <img :src="product.thumbnail" class="h-56 w-auto mx-auto" alt="" />
        <div class="p-5">
          <span class="text-gray-800 text-lg font-bold">{{
            product.title
          }}</span>

          <div class="flex justify-between items-center my-2">
            <p>$ {{ product.price }}</p>
            <a
              href="#"
              class="hover:border-b-2 flex justify-between items-center"
              >Add to
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="1.5"
                stroke="currentColor"
                class="w-5 h-5"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M2.25 3h1.386c.51 0 .955.343 1.087.835l.383 1.437M7.5 14.25a3 3 0 00-3 3h15.75m-12.75-3h11.218c1.121-2.3 2.1-4.684 2.924-7.138a60.114 60.114 0 00-16.536-1.84M7.5 14.25L5.106 5.272M6 20.25a.75.75 0 11-1.5 0 .75.75 0 011.5 0zm12.75 0a.75.75 0 11-1.5 0 .75.75 0 011.5 0z"
                />
              </svg>
            </a>
          </div>

          <div class="flex justify-between items-center mt-4">
            <router-link
              :to="{ name: 'productDetails', params: { id: product.id } }"
              :class="detailsBtn"
              type="submit"
              >View Details
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
