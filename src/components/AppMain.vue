<template>
  <main>
    <section>
      <div class="container">
        <h1>Film</h1>
        <div class="row">
          <FilmCard v-for="film in films" :key="film.id" :film="film" />
        </div>
      </div>
    </section>
    <section>
      <div class="container">
        <h1>Serie TV</h1>
        <div class="row">
          <TVsCard v-for="serie in TVs" :key="serie.id" :serie="serie" />
        </div>
      </div>
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
