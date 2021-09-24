<template>
  <!-- invio !! 
    PAdrE/ FIGLIO, con APP.VUE-- MAIN
    passo PROPS 
-->
  <!-- riceve !! 
    FIGLIO/ PADRE, da HEADER 
    passo EMIT 
-->
  <div>
    <section class="container">
      <!-- <div v-if="!loading"> -->
        <div>
        <!-- HEADER  richiamo evento click EMIT-->
        <Header @search="searchMovie" />
        <!-- MAIN  -->
        <div v-for="(movie, index) in filteredMoviesList" :key="index">
          <Main :key="index" :moviesProps="movie" />
        </div>
      </div>

      <!-- <Loader v-else /> -->
    </section>
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
// import Loader from "./components/Loader.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
    // Loader,
  },
  data() {
    return {
      // axios call & get movie
      ApiUrl: "https://api.themoviedb.org/3/search/movie?api_key=",
      ApiKey: "067b4cde552c058a889d074fbf25bd57&query=",
      queryText: "",
      // search
      movieList: [],
      // loader
      // loading: true,
    };
  },
  methods: {
    // function GET movie
    getMovie() {
      axios
        .get(this.ApiUrl + this.ApiKey + this.querytext)
        .then((res) => {
          for (let i = 0; i < this.movieList.length; i++) {
            let movie = res.data.results[i].movie;
            // console.log(res.data.results[i].movie);
            if (!this.movieList.includes(movie)) {
              this.movieList.push(movie);
              // console.log(this.movieList);
            }
          }
          // setTimeout(() => {
          //   this.loading = false;
          // }, 2000);
        })
        .catch((err) => {
          console.log("Doesn't work ", err);
        });
    },
    searchMovie(text) {
      this.querytext = text;
    },
    // definisco funzione che collega a metodo
  },
  computed: {
    // function FILTER MOVIE LIST
    filteredMoviesList() {
      if (this.queryText === "") {
        return this.moviesList;
      }

      let filteredList = this.moviesList.filter((element) => {
        return element.name
          .toLowerCase()
          .includes(this.queryText.toLowerCase());
      });

      return filteredList;
    },
  },
  created() {
    this.getMovie();
  },
};
</script>

<style lang="scss">
@import "@/styles/mixin.scss";
@import "@/styles/general.scss";
@import "@/styles/vars.scss";

#app {
  width: 100%;
}
</style>
