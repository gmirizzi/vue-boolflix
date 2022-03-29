<template>
  <main>
    <section>
      <h1>Film</h1>
      <FilmCard v-for="film in films" :key="film.id" :film="film" />
    </section>
    <section>
      <h1>Serie TV</h1>
      <TVsCard v-for="serie in TVs" :key="serie.id" :serie="serie" />
    </section>
  </main>
</template>

<script>
import FilmCard from "./FilmCard.vue";
import TVsCard from "./TVsCard.vue";

export default {
  name: "AppMain",
  components: {
    TVsCard,
    FilmCard,
  },
  props: {
    films: Array,
    TVs: Array,
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
    this.TVs.forEach((element) => {
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
