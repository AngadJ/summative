<script setup>
import axios from "axios";
import { useStore } from "../store/index.js";

const store = useStore();
const props = defineProps(["id"]);
const emits = defineEmits(["toggleModal"]);

let data = (
  await axios.get(`https://api.themoviedb.org/3/movie/${props.id}`, {
    params: {
      api_key: "f944b70daa59b60504fca0c383e63483",
      append_to_response: "videos",
    },
  })
).data;
</script>

<template>
  <Teleport to="body">
    <div class="modal-outer-container" @click.self="emits('toggleModal')">
      <div class="modal-inner-container">
        <button class="close-button" @click="emits('toggleModal')">X</button>
        <img
          :src="`https://image.tmdb.org/t/p/w500${data.poster_path}`"
          alt=""
        />
        <p>{{ data.original_title }}</p>
        <p>Release Date: {{ data.release_date }}</p>
        <p>Rating: {{ data.vote_average }} Stars</p>
        <p>Popularity: {{ data.popularity }}</p>
        <p>Box Office: {{ data.revenue }} USD</p>
        <p>
          <a
            :href="`https://www.youtube.com/embed/${
              data.videos.results
                .filter((video) => video.type === 'Trailer')
                .at(0).key
            }`"
            target="_blank"
          >
            Here to View the Movie Trailer!
          </a>
        </p>
        <div class="purchaseButton-container">
          <button @click="
            store.addToCart(props.id, {
              id: data.id,
              poster: data.poster_path,
              title: data.title,
              date: data.release_date,
            })
          ">
            Add To Cart
          </button>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.modal-outer-container {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background: #00000099;
  z-index: 3;
  font-size: 19px;
  font-family: "Kalam", cursive;
  text-align: center;
}
.modal-outer-container .modal-inner-container {
  background-color: rgb(29, 28, 28);
  color: white;
  width: clamp(280px, 100%, 800px);
  height: 400px;
  position: relative;
}
.modal-outer-container .modal-inner-container .close-button {
  position: absolute;
  right: 0px;
  padding: 1rem;
  border: none;
  background: #1f2123;
  font-weight: bold;
  font-size: 1.25rem;
  color: white;
}
img {
  width: 280px;
  height: 400px;
  float: right;
  border-style: solid;
  border-color: rgb(58, 186, 237);
  border-width: 2px;
}
button {
  font-size: 20px;
  padding: 10px;
  font-family: "Zen Dots", cursive;
}
</style>
