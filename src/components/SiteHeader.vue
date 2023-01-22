<script setup></script>

<template>
  <div>
    <h1>AJ's Movies4u</h1>
    <RouterLink to="/login" custom v-slot="{ navigate }">
      <button @click="navigate" role="link">Login</button>
    </RouterLink>
  </div>
</template>

<style scoped>
h1 {
  color: white;
  font-family: "Bangers", cursive;
  font-size: 50px;
  border-color: rgb(58, 186, 237);
  border-width: 15px;
  border-style: double;
  padding: 20px;
  width: 290px;
  margin-left: 20px;
  text-align: center;
}

button {
  position: relative;
  bottom: 125px;
  left: 400px;
  padding: 20px;
  font-family: "Play", sans-serif;
  font-size: 25px;
  font-weight: bolder;
}

:hover {
  border-width: 15px;
  border-color: rgb(58, 186, 237);
}
</style>
