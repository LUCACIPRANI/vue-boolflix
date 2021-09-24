<template>
  <!-- RICEVO !! 
    FIGLIO/ PADRE, da APP.VUE 
    passo PROPS 
-->
  <main>
    <div class="movie">
      <h4>{{ moviesProps.title }}</h4>
      <div>{{ moviesProps.original_title }}</div>
      <div>{{ moviesProps.original_language }}</div>
      <div>{{ moviesProps.vote_average }}</div>
    </div>
  </main>
</template>

<script>
export default {
  name: "Main",
  props: ["moviesProps"],
  data() {
    return {
    };
  },
  mounted() {},
  computed() {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/styles/mixin.scss";
@import "@/styles/general.scss";
@import "@/styles/vars.scss";
</style>
