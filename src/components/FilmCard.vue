<template>
  <div class="col-4">
    <div class="item p-4 border border-white">
      <div class="poster h-100">
        <img
          :src="`https://image.tmdb.org/t/p/w342` + film.poster_path"
          :alt="`Copertina ` + film.title"
          class="img-fluid h-100"
        />
      </div>
      <div class="info">
        <div class="title">
          <span class="fw-bold">Titolo: </span>{{ film.title }}
        </div>
        <div class="original-title" v-show="film.original_title != film.title">
          <span class="fw-bold">Titolo originale: </span
          >{{ film.original_title }}
        </div>
        <div class="lang">
          <span class="fw-bold">Lingua: </span>
          <i
            v-if="this.languageseSwitchCases.includes(film.original_language)"
            :class="film.original_language"
          ></i>
          <span v-else>{{ film.original_language }}</span>
        </div>
        <div class="rate">
          <span class="fw-bold">Voto: </span>
          <font-awesome-icon
            v-for="n in film.vote_average"
            icon="fa-solid fa-star"
            :key="n"
            class="text-warning"
          />
          <font-awesome-icon
            v-for="n in 5 - film.vote_average"
            icon="fa-regular fa-star"
            :key="n"
            class="text-warning"
          />
        </div>
        <div class="overview" v-show="film.overview">
          <span class="fw-bold">Overview: </span>{{ film.overview }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FilmCard",
  data() {
    return {
      languageseSwitchCases: [
        "flag flag-united-kingdom",
        "flag flag-italy",
        "flag flag-france",
      ],
    };
  },
  props: {
    film: Object,
  },
};
</script>

<style lang="scss" scoped></style>
