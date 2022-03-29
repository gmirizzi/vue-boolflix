<template>
  <div class="card">
    <div class="name">{{ serie.name }}</div>
    <div class="original-name">{{ serie.original_name }}</div>
    <div class="lang">
      <i
        v-if="this.languageseSwitchCases.includes(serie.original_language)"
        :class="serie.original_language"
      ></i>
      <span v-else>{{ serie.original_language }}</span>
    </div>
    <div class="rate">{{ serie.vote_average }}</div>
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
</style>
