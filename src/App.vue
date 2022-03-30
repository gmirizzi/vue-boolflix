<template>
  <div id="app">
    <header class="d-flex justify-content-between align-items-center p-2">
      <h1>BOOLFLIX</h1>
      <SearchBar @getFilms="populeArrayFilms" @getTVs="populeArrayTVs" />
    </header>
    <AppMain :films="arrFilms" :TVs="arrTVs" />
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar.vue";
import AppMain from "./components/AppMain.vue";

export default {
  name: "App",
  components: {
    AppMain,
    SearchBar,
  },
  data() {
    return {
      arrFilms: [],
      arrTVs: [],
    };
  },
  methods: {
    populeArrayFilms(searchedFilms) {
      return (this.arrFilms = searchedFilms);
    },
    populeArrayTVs(searchedTVs) {
      return (this.arrTVs = searchedTVs);
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
