<template>
  <main>
    <FilmCard v-for="film in films" :key="film.id" :film="film" />
  </main>
</template>

<script>
import FilmCard from "./FilmCard.vue";

export default {
  name: "AppMain",
  components: {
    FilmCard,
  },
  props: {
    films: Array,
  },
};
</script>

<style></style>
