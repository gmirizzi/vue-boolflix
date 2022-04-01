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
        <div class="cast" v-show="arrNames.length > 0">
          <span class="fw-bold">Cast: </span>
          <ul>
            <li v-for="actor in arrNames" :key="actor">{{ actor }}</li>
          </ul>
        </div>
        <div class="genres" v-show="serie.genres">
          <span class="fw-bold">Generi: </span>{{ serie.genres }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "TVsCard",
  data() {
    return {
      languageseSwitchCases: [
        "flag flag-united-kingdom",
        "flag flag-italy",
        "flag flag-france",
      ],
      arrNames: [],
    };
  },
  props: {
    serie: Object,
  },
  created() {
    axios
      .get(
        `https://api.themoviedb.org/3/tv/${this.serie.id}/aggregate_credits?api_key=01af620fbe2924c05e6048caa6f5c225`
      )
      .then((response) => {
        const cast = response.data.cast;
        if (cast.length > 0) {
          const castNames = [];
          if (cast.length <= 5) {
            cast.forEach((el) => castNames.push(el.name));
            this.arrNames = castNames;
          } else {
            for (let index = 0; index <= 4; index++) {
              castNames.push(cast[index].name);
            }
            this.arrNames = castNames;
          }
        }
      });
  },
};
</script>

<style lang="scss" scoped></style>
