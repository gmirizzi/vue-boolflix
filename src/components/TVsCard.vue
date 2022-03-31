<template>
  <div class="col-4">
    <div class="item p-4 border border-white">
      <div class="poster h-100">
        <img
          :src="`https://image.tmdb.org/t/p/w342` + serie.poster_path"
          :alt="`Copertina ` + serie.name"
          class="img-fluid h-100"
        />
      </div>
      <div class="info">
        <div class="name">
          <span class="fw-bold">Titolo: </span>{{ serie.name }}
        </div>
        <div class="original-name" v-show="serie.original_name != serie.name">
          <span class="fw-bold">Titolo originale: </span
          >{{ serie.original_name }}
        </div>
        <div class="lang">
          <span class="fw-bold">Lingua: </span>
          <i
            v-if="this.languageseSwitchCases.includes(serie.original_language)"
            :class="serie.original_language"
          ></i>
          <span v-else>{{ serie.original_language }}</span>
        </div>
        <div class="rate">
          <span class="fw-bold">Voto: </span>
          <font-awesome-icon
            v-for="n in serie.vote_average"
            icon="fa-solid fa-star"
            :key="n"
            class="text-warning"
          />
          <font-awesome-icon
            v-for="n in 5 - serie.vote_average"
            icon="fa-regular fa-star"
            :key="n"
            class="text-warning"
          />
        </div>
        <div class="overview" v-show="serie.overview">
          <span class="fw-bold">Overview: </span>{{ serie.overview }}
        </div>
        <div class="cast">
          <span class="fw-bold">Cast: </span>
          <ul>
            <li v-for="actor in serie.cast" :key="actor">{{ actor }}</li>
          </ul>
        </div>
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

<style lang="scss" scoped></style>
