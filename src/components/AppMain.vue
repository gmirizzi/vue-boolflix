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
      <section v-show="filmFilter.length > 0" class="py-5">
        <div class="container">
          <h1>Film</h1>
          <div class="row gy-5">
            <FilmCard v-for="film in filmFilter" :key="film.id" :film="film" />
          </div>
        </div>
      </section>
      <section v-show="tvsFilter.length > 0" class="py-5">
        <div class="container">
          <h1>Serie TV</h1>
          <div class="row gy-5">
            <TVsCard
              v-for="serie in tvsFilter"
              :key="serie.id"
              :serie="serie"
            />
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
    selectedGenre: String,
  },
  computed: {
    filmFilter() {
      if (this.selectedGenre == "") {
        return this.films;
      } else {
        return this.films.filter((film) =>
          film.genres.includes(this.selectedGenre)
        );
      }
    },
    tvsFilter() {
      if (this.selectedGenre == "") {
        return this.TVs;
      } else {
        return this.TVs.filter((tv) => tv.genres.includes(this.selectedGenre));
      }
    },
  },
  data() {
    return {
      genres: [],
    };
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
    this.films.forEach((element) => {
      axios
        .get(
          `https://api.themoviedb.org/3/movie/${element.id}?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT`
        )
        .then((response) => {
          element.genres = response.data.genres.map((el) => el.name);
        });
    });
    this.TVs.forEach((element) => {
      axios
        .get(
          `https://api.themoviedb.org/3/tv/${element.id}?api_key=01af620fbe2924c05e6048caa6f5c225&language=it-IT`
        )
        .then((response) => {
          element.genres = response.data.genres.map((el) => el.name);
        });
    });
    this.TVs.forEach((element) => {
      return (element.vote_average = Math.floor(element.vote_average / 2) + 1);
    });
  },
};
</script>

<style lang="scss">
.item {
  overflow: auto;
  background-color: black;
  height: 500px;
  transition: transform 1.6s;
  .info {
    display: none;
    transform: rotateY(360deg);
    transition: all 1.6s;
  }
  &:hover {
    transform: rotateY(360deg);
    .poster {
      display: none;
    }
    .info {
      display: block;
    }
  }
}
</style>
