<template>
  <div class="card">
    <div class="title">{{ film.title }}</div>
    <div class="original-title">{{ film.original_title }}</div>
    <div class="lang">{{ film.original_language }}</div>
    <div class="rate">{{ film.vote_average }}</div>
  </div>
</template>

<script>
export default {
  name: "FilmCard",
  props: {
    film: Object,
  },
};
</script>

<style></style>
