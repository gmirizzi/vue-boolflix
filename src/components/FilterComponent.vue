<template>
  <select name="" id="">
    <option value="">Seleziona un genere</option>
    <option v-for="genre in genres" :key="genre.id" :value="genre.name">
      {{ genre.name }}
    </option>
  </select>
</template>

<script>
import axios from "axios";

export default {
  name: "FilterComponent",
  data() {
    return {
      genres: [],
    };
  },
  beforeCreate() {
    axios
      .get(
        "https://api.themoviedb.org/3/genre/movie/list?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT"
      )
      .then((res) => (this.genres = res.data.genres));
  },
};
</script>

<style></style>
