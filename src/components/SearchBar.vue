<template>
  <div>
    <form @submit.prevent="searchTVs(), searchFilms()">
      <input type="search" v-model="query" />
      <button>Cerca</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SearchBar",
  data() {
    return {
      query: "",
      searchedFilms: [],
      searchedTVs: [],
    };
  },
  methods: {
    searchFilms() {
      if (this.query != "") {
        axios
          .get(
            `https://api.themoviedb.org/3/search/movie?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT&query=${this.query}`
          )
          .then((response) => {
            this.searchedFilms = response.data.results;
            this.$emit("getFilms", this.searchedFilms);
          });
      }
    },
    searchTVs() {
      if (this.query != "") {
        axios
          .get(
            `https://api.themoviedb.org/3/search/tv?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT&page=1&query=${this.query}`
          )
          .then((response) => {
            this.searchedTVs = response.data.results;
            this.$emit("getTVs", this.searchedTVs);
          });
      }
    },
  },
};
</script>

<style lang="scss"></style>
