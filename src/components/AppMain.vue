<template>
  <div
    id="default"
    v-if="submitted == false"
    class="text-white text-center m-5 fw-bold text-uppercase"
  >
    Benvenuto
  </div>
  <div v-else>
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
  </div>
</template>

<script>
import TVsCard from "./TVsCard.vue";
import FilmCard from "./FilmCard";
import axios from "axios";

export default {
  name: "AppMain",
  components: {
    TVsCard,
    FilmCard,
  },
  props: {
    films: Array,
    TVs: Array,
    submitted: Boolean,
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
    this.TVs.forEach((element) => {
      axios
        .get(
          `https://api.themoviedb.org/3/tv/${element.id}/aggregate_credits?api_key=01af620fbe2924c05e6048caa6f5c225`
        )
        .then((response) => {
          const cast = response.data.cast;
          const castNames = [];
          if (cast.length > 0) {
            if (cast.length <= 5) {
              cast.forEach((el) => castNames.push(el.name));
              element.cast = castNames;
            } else {
              for (let index = 0; index <= 4; index++) {
                castNames.push(cast[index].name);
              }
              element.cast = castNames;
            }
          }
        });
    });
  },
};
</script>

<style lang="scss">
.item {
  overflow: auto;
  background-color: black;
  height: 500px;
  .info {
    display: none;
  }
  &:hover {
    .poster {
      display: none;
    }
    .info {
      display: block;
    }
  }
}
</style>
