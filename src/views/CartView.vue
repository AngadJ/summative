<script setup>
import { useStore } from "../store/index.js";
const store = useStore();
</script>

<template>
  <div v-for="movie in Array.from(store.cart.values())">
    <img :src="`https://image.tmdb.org/t/p/w500${movie.poster}`" />
    <h1>{{ movie.title }}</h1>
    <h1>{{ movie.date }}</h1>
    <button @click="store.removeFromCart(movie.id)">Remove</button>
  </div>
</template>

<style scoped>
img {
  width: 280px;
  height: 400px;
  border-style: double;
  border-color: rgb(58, 186, 237);
  border-width: 15px;
}

h1 {
  font-size: 30px;
  color: rgb(58, 186, 237);
}

button {
  font-size: 20px;
  padding: 10px;
  font-family: "Zen Dots", cursive;
  margin-bottom: 20px;
}
</style>
