<script setup>
import { RouterView } from "vue-router";
import HeaderSection from "./components/HeaderSection.vue";
import Footer from "./components/FooterSection.vue";
</script>

<template>
  <HeaderSection />

  <RouterView />

  <Footer />
</template>

<style scoped></style>
