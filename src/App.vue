<template>
  <div>
    <section id="app">
      <div v-if="!loading">
        <!-- HEADER richiamo evento click EMIT impostato -->
        <Header @performSearch="search" />
        <!-- MAIN  -->
        <div 
          v-for="(tv, index) in tvList" 
          :key="index"
        >
          <Main :key="index" :info="tv" />
        </div>

        <div
          v-for="(movie, index) in movieList"
          :key="index"
        >
          <Main :key="index" :info="movie" />
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
      ApiUrlMovie: "https://api.themoviedb.org/3/search/movie?api_key=",
      ApiUrlSeries: "https://api.themoviedb.org/3/search/tv?api_key=",
      ApiKey: "067b4cde552c058a889d074fbf25bd57&query=",
      queryText: "",
      movieList: [],
      tvList: [],
      loading: true,
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
          console.log(res.data.results);
          if (res.data.results.length > 0) {
            for (let i = 0; i < res.data.results.length; i++) {
              let movie = res.data.results[i];
              if (!this.movieList.includes(movie)) {
                this.movieList.push(movie);
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
          console.log(res.data.results);
          if (res.data.results.length > 0) {
            for (let i = 0; i < res.data.results.length; i++) {
              let movie = res.data.results[i];
              if (!this.tvList.includes(movie)) {
                this.tvList.push(movie);
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
