<template>
  <div id="app">
    <header class="d-flex justify-content-between align-items-center p-2">
      <h1>BOOLFLIX</h1>
      <div class="d-flex">
        <SearchBar
          @getFilms="populeArrayFilms"
          @getTVs="populeArrayTVs"
          @searchOn="searchOn"
        />
        <FilterComponent class="ms-3" />
      </div>
    </header>
    <AppMain :films="arrFilms" :TVs="arrTVs" :submitted="submitted" />
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
    };
  },
  methods: {
    populeArrayFilms(searchedFilms) {
      return (this.arrFilms = searchedFilms);
    },
    populeArrayTVs(searchedTVs) {
      return (this.arrTVs = searchedTVs);
    },
    searchOn(searchBarSubmitted) {
      this.submitted = searchBarSubmitted;
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
