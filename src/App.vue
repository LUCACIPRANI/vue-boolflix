<template>
  <div>
    <section id="app">
      <div v-if="!loading">
        <!-- HEADER richiamo evento click EMIT impostato -->
        <Header @performSearch="search" />
       <!-- POPULAR on netflix  -->
        <div v-if="queryText ==''">
          <Popular>
            <div 
              v-for="(popular) in populars" 
              :key="popular.id"
              >
              <Main :key="popular.id" :info="popular" />
            </div>
          </Popular>
        </div>
           <!-- MAIN  -->
        <div v-else>
          <div 
            v-for="(tv) in tvList" 
            :key="tv.id"
          >
            <Main :key="tv.id" :info="tv" />
          </div>

          <div
            v-for="(movie) in movieList"
            :key="movie.id"
          >
            <Main :key="movie.id" :info="movie" />
          </div>
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
import Popular from "./components/Popular.vue";


export default {
  name: "App",
  components: {
    Header,
    Main,
    Popular,
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
      ApiUrlPopular: "https://api.themoviedb.org/3/person/popular?api_key=",
      page: "page=1",
      populars: [],
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
    getPopular() {
      axios
        .get(this.ApiUrlPopular + this.ApiKey + this.queryText + this.page)
        .then((res) => {
          console.log(res.data.results);
          if (res.data.results.length > 0) {
            for (let i = 0; i < res.data.results.length; i++) {
              let movie = res.data.results[i];
              if (!this.populars.includes(movie)) {
                this.populars.push(movie);
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
@import '~@fortawesome/fontawesome-free/css/all.min.css';
@import "@/styles/mixin.scss";
@import "@/styles/general.scss";
@import "@/styles/vars.scss";

#app {
  height: 100vh;
  margin: 0 auto;
  text-align: center;
}
</style>
