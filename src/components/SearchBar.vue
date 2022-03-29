<template>
  <div>
    <input type="search" v-model="query" />
    <button @click="search">Cerca</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "SearchBar",
  data() {
    return {
      query: "",
    };
  },
  methods: {
    search() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT&query=${this.query}`
        )
        .then((response) => {
          console.log(response);
        });
    },
  },
};
</script>

<style></style>
