<template>
  <div id="app">
    <header class="d-flex justify-content-between align-items-center p-2">
      <h1>BOOLFLIX</h1>
      <div class="d-flex align-items-center">
        <SearchBar
          @getFilms="populeArrayFilms"
          @getTVs="populeArrayTVs"
          @searchOn="searchOn"
        />
        <FilterComponent @filtra="getGenre" class="ms-3" />
      </div>
    </header>
    <AppMain
      :films="arrFilms"
      :TVs="arrTVs"
      :submitted="submitted"
      :selectedGenre="genre"
    />
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import AppMain from "./components/AppMain.vue";
import FilterComponent from "./components/FilterComponent.vue";

export default {
  name: "App",
  components: {
    AppMain,
    SearchBar,
    FilterComponent,
  },
  data() {
    return {
      arrFilms: [],
      arrTVs: [],
      submitted: false,
      genre: "",
    };
  },
  methods: {
    getGenre(selected) {
      this.genre = selected;
    },
    populeArrayFilms(searchedFilms) {
      return (this.arrFilms = searchedFilms);
    },
    populeArrayTVs(searchedTVs) {
      return (this.arrTVs = searchedTVs);
    },
    searchOn(searchBarSubmitted, resetGenre) {
      this.submitted = searchBarSubmitted;
      this.genre = resetGenre;
    },
  },
};
</script>

<style lang="scss">
@import "~mdb-ui-kit/css/mdb.min.css";
#app {
  background-color: #434343;
  min-height: 100vh;
  header {
    background-color: black;
    h1 {
      color: red;
    }
  }
}
</style>
