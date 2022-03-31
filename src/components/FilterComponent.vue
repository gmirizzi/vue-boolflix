<template>
  <div>
    <label for="select" class="text-white me-2">Seleziona un genere: </label>
    <select name="" id="select">
      <option value="">All</option>
      <optgroup label="Film">
        <option v-for="genre in filmGenres" :key="genre.id" :value="genre.name">
          {{ genre.name }}
        </option>
      </optgroup>
      <optgroup label="Serie Tv">
        <option v-for="genre in tvsGenres" :key="genre.id" :value="genre.name">
          {{ genre.name }}
        </option>
      </optgroup>
    </select>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "FilterComponent",
  data() {
    return {
      filmGenres: [],
      tvsGenres: [],
    };
  },
  beforeCreate() {
    axios
      .get(
        "https://api.themoviedb.org/3/genre/movie/list?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT"
      )
      .then((res) => (this.filmGenres = res.data.genres));
    axios
      .get(
        "https://api.themoviedb.org/3/genre/tv/list?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT"
      )
      .then((res) => (this.tvsGenres = res.data.genres));
  },
};
</script>

<style></style>
