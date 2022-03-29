<template>
  <div id="app">
    <SearchBar @getFilms="populeArrayFilms" @getTVs="populeArrayTVs" />
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
      arrFilms: null,
      arrTVs: null,
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

<style lang="scss"></style>
