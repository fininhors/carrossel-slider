<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from "vue";
import Carrossel from "./components/carrossel/Carrossel.vue";


const slides = ref([
  "https://picsum.photos/id/1018/1024/768.jpg",
  "https://picsum.photos/id/1019/1024/768.jpg",
  "https://picsum.photos/id/102/1024/768.jpg",
  "https://picsum.photos/id/1050/1024/768.jpg",
  "https://picsum.photos/id/110/1024/768.jpg"
]);

</script>

<template>
  <Carrossel :slides="slides" :indicators="true" :controls="true" :interval="5000" />
</template>

<style>
</style>
