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
  updated() {
    this.films.forEach((element) => {
      switch (element.original_language) {
        case "en":
          return (element.original_language = "flag flag-united-kingdom");
        case "it":
          return (element.original_language = "flag flag-italy");
        case "fr":
          return (element.original_language = "flag flag-france");
        default:
          return element.original_language;
      }
    });
  },
};
</script>

<style lang="scss" scoped></style>
