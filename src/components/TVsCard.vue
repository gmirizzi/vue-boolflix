<template>
  <div class="card">
    <img
      :src="`https://image.tmdb.org/t/p/w342` + serie.poster_path"
      :alt="`Copertina ` + serie.name"
    />
    <div class="name">{{ serie.name }}</div>
    <div class="original-name">{{ serie.original_name }}</div>
    <div class="lang">
      <i
        v-if="this.languageseSwitchCases.includes(serie.original_language)"
        :class="serie.original_language"
      ></i>
      <span v-else>{{ serie.original_language }}</span>
    </div>
    <div class="rate">
      <div class="rate">
        <font-awesome-icon
          v-for="n in serie.vote_average"
          icon="fa-solid fa-star"
          :key="n"
        />
        <font-awesome-icon
          v-for="n in 5 - serie.vote_average"
          icon="fa-regular fa-star"
          :key="n"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TVsCard",
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
    serie: Object,
  },
};
</script>

<style lang="scss" scoped>
@import "~mdb-ui-kit/css/mdb.min.css";
img {
  width: 100px;
}
</style>
