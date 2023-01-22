<script setup>
import { ref } from "vue";
import SiteFooter from "../components/SiteFooter.vue";
import SiteModal from "../components/SiteModal.vue";
import { useStore } from "../store/index.js";

const store = useStore();
const genre = ref(28);
const showModal = ref(false);
const selectedId = ref(0);

const openModal = (id) => {
  showModal.value = true;
  selectedId.value = id;
};

const closeModal = () => {
  showModal.value = false;
};

const getGenres = async () => {
  await store.getMovies(genre.value);
};
</script>

<template>
  <div>
    <h1>
      Wondering what movie to watch next? <br />
      Here are several genres to choose from, click on the movie to get some
      cool info!
    </h1>
    <h2>Genres:</h2>
  </div>
  <select v-model="genre" class="dropdown" @change="getGenres()">
    <option value="28">Action</option>
    <option value="12">Adventure</option>
    <option value="878">Science Fiction</option>
    <option value="16">Animation</option>
    <option value="35">Comedy</option>
    <option value="80">Crime</option>
    <option value="18">Drama</option>
    <option value="10751">Family</option>
    <option value="14">Fantasy</option>
    <option value="36">History</option>
    <option value="27">Horror</option>
    <option value="10402">Music</option>
    <option value="9648">Mystery</option>
    <option value="10749">Romance</option>
    <option value="10770">TV Movie</option>
    <option value="53">Thriller</option>
    <option value="10752">War</option>
    <option value="37">Western</option>
  </select>

  <RouterLink to="/cart" custom v-slot="{ navigate }">
    <button @click="navigate" role="link">Cart</button>
  </RouterLink>

  <div class="purchase-container">
    <img
      v-for="movie in store.movies"
      :id="movie.id"
      @click="openModal(movie.id)"
      :src="`https://image.tmdb.org/t/p/w500${movie.poster}`"
    />
    <SiteModal v-if="showModal" @toggleModal="closeModal()" :id="selectedId" />
  </div>
  
  <div>
    <SiteFooter />
  </div>
</template>

<style scoped>
h1 {
  color: white;
  border-color: rgb(58, 186, 237);
  border-width: 15px;
  border-style: double;
  font-family: "Zen Dots", cursive;
  padding: 20px;
  font-size: 25px;
  margin-right: 250px;
}

h2 {
  color: white;
  border-color: rgb(58, 186, 237);
  border-width: 10px;
  border-style: double;
  font-family: "Zen Dots", cursive;
  padding: 20px;
  font-size: 25px;
  margin-right: 1200px;
}
.purchase-container {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 1rem;
}
img {
  width: 200px;
  border-style: double;
  border-color: rgb(58, 186, 237);
  border-width: 15px;
  margin-right: 10px;
  margin-top: 15px;
}
img:hover {
  border-color: white;
}
button:hover {
  border-color: white;
}
button {
  padding: 10px;
  height: 100px;
  width: 170px;
  font-size: 50px;
  font-family: "Courgette", cursive;
  border-color: white;
  border-width: 5px;
  position: relative;
  top: -260px;
  left: 920px;
}
.dropdown {
  padding: 10px;
  width: 250px;
  font-size: 20px;
  font-family: "Zen Dots", cursive;
  border-color: rgb(58, 186, 237);
  border-width: 5px;
  margin-left: 10px;
  position: relative;
  bottom: 130px;
  left: 200px;
}
.footer {
  font-size: 15px;
  font-family: "Play", sans-serif;
  text-align: center;
  padding: 3px;
  background-color: rgb(58, 186, 237);
  color: navy;
  position: relative;
  top: 30px;
}

button:hover {
  border-color: rgb(58, 186, 237);
  border-width: 15px;
}
</style>
