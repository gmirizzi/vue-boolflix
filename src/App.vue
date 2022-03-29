<template>
  <div id="app">
    <SearchBar @getFilms="populeArrayFilms" />
    <AppMain :films="arrFilms" />
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
    };
  },
  methods: {
    populeArrayFilms(searchedFilms) {
      return (this.arrFilms = searchedFilms);
    },
  },
};
</script>

<style lang="scss"></style>
