<template>
  <div>
    <input type="search" v-model="query" />
    <button @click="searchTVs(), searchFilms()">Cerca</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SearchBar",
  data() {
    return {
      query: "",
      searchedFilms: null,
      searchedTVs: null,
    };
  },
  methods: {
    searchFilms() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT&query=${this.query}`
        )
        .then((response) => {
          this.searchedFilms = response.data.results;
          console.log(this.searchedFilms);
          this.$emit("getFilms", this.searchedFilms);
        });
    },
    searchTVs() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT&page=1&query=${this.query}`
        )
        .then((response) => {
          this.searchedTVs = response.data.results;
          console.log(this.searchedTVs);
          this.$emit("getTVs", this.searchedTVs);
        });
    },
  },
};
</script>

<style></style>
