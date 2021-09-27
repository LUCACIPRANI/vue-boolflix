<template>
  <div>
    <section id="app" class="container">
      <div v-if="!loading">
        <!-- HEADER  richiamo evento click EMIT impostato nell'header-->
        <Header 
          @performSearch="search" 
        />
        <!-- MAIN  -->
        <div class="container" 
        v-for="(movie, index) in movieList" 
        :key="index">
          <Main :key="index" 
          :moviesProps="movie" 
          :tvProps="movie"
          />
          
        </div>
      </div>
      <Loader v-else />
    </section>
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import Loader from "./components/Loader.vue";

export default {
  name: "App",
  components: {
    Header,
    Main,
    Loader,
  },
  data() {
    return {
      // axios call & get movie
      ApiUrlMovie: "https://api.themoviedb.org/3/search/movie?api_key=",
      ApiKey: "067b4cde552c058a889d074fbf25bd57&query=",
      ApiUrlSeries: "https://api.themoviedb.org/3/search/tv?api_key=",
      queryText: "",
      movieList: [],
      tvList: [],
      // LOADER
      loading: false,
    };
  },
  created() {
    setTimeout(() => {
      this.loading = false;
    }, 1000);
  },
  methods: {
    getMovie() {
      axios
        .get(this.ApiUrlMovie + this.ApiKey + this.queryText)
        .then((res) => {
          if (res.data.results.length > 0) {
            for (let i = 0; i < res.data.results.length; i++) {
              let movie = res.data.results[i];
              if (!this.movieList.includes(movie)) {
                this.movieList.push(movie);
                console.log(this.movieList);
              }
            }
          }
        })
        .catch((err) => {
          console.log("Doesn't work ", err);
        });
    },
    getTv() {
      axios
        .get(this.ApiUrlSeries + this.ApiKey + this.queryText)
        .then((res) => {
          if (res.data.results.length > 0) {
            for (let i = 0; i < res.data.results.length; i++) {
              let movie = res.data.results[i];
              if (!this.tvList.includes(movie)) {
                this.tvList.push(movie);
                console.log(this.tvList);
              }
            }
          }
        })
        .catch((err) => {
          console.log("Doesn't work ", err);
        });
    },
    // definisco funzione per catturare evento
    search(text) {
      this.queryText = text;
      this.getMovie();
      this.getTv();
    },
  },
  computed: {
    filteredMoviesList() {
      if (this.queryText === " ") {
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
};
</script>

<style lang="scss">
@import "@/styles/mixin.scss";
@import "@/styles/general.scss";
@import "@/styles/vars.scss";

#app {
  height: 100vh;
  margin: 0 auto;
  text-align: center;
}
</style>
