<template>
  <main class="text-white">
    <section v-show="films.length > 0" class="py-5">
      <div class="container">
        <h1>Film</h1>
        <div class="row gy-5">
          <FilmCard v-for="film in films" :key="film.id" :film="film" />
        </div>
      </div>
    </section>
    <section v-show="TVs.length > 0" class="py-5">
      <div class="container">
        <h1>Serie TV</h1>
        <div class="row gy-5">
          <TVsCard v-for="serie in TVs" :key="serie.id" :serie="serie" />
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import TVsCard from "./TVsCard.vue";
import FilmCard from "./FilmCard";

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
    this.films.forEach((element) => {
      return (element.vote_average = Math.floor(element.vote_average / 2) + 1);
    });
    this.TVs.forEach((element) => {
      return (element.vote_average = Math.floor(element.vote_average / 2) + 1);
    });
  },
};
</script>

<style lang="scss" scoped></style>
