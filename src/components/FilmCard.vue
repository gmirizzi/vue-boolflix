<template>
  <div class="card">
    <img
      :src="`https://image.tmdb.org/t/p/w342` + film.poster_path"
      :alt="`Copertina ` + film.name"
    />
    <div class="title">{{ film.title }}</div>
    <div class="original-title">{{ film.original_title }}</div>
    <div class="lang">
      <i
        v-if="this.languageseSwitchCases.includes(film.original_language)"
        :class="film.original_language"
      ></i>
      <span v-else>{{ film.original_language }}</span>
    </div>
    <div class="rate">{{ film.vote_average }}</div>
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

<style lang="scss" scoped>
@import "~mdb-ui-kit/css/mdb.min.css";
img {
  width: 100px;
}
</style>
