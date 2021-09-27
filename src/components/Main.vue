<template>
  <div class="main-container">
    <!-- movies  -->
    <div class="cards-movie">
      <h4>Movie</h4>
      <div>
        <img src="require(`imageURL${moviesProps.backdrop_path}`)" alt="">
      </div>
      <h4><span>Title</span> {{ moviesProps.title }}</h4>
      <h4><span>Original Title: </span> {{ moviesProps.original_title }}</h4>
      <div>
        <span>Language: </span>
        <img
          :src="require(`../assets/img/${moviesProps.original_language}.png`)"
        />
      </div>
      <div><span> Reviews: </span>{{ moviesProps.vote_average }}</div>
    </div>
    <!-- tv series  -->
    <div class="cards-tv">
      <h4>TV Series</h4>
      <div>
        <img src="require(`imageURL${tvProps.backdrop_path}`)" alt="">
      </div>
      <h4><span>Name:</span> {{ tvProps.name }}</h4>
      <h4><span>Original Name: </span> {{ tvProps.original_name }}</h4>
      <div>
        <span>Language: </span>
        <img :src="require(`../assets/img/${tvProps.original_language}.png`)" />
      </div>
      <div><span> Reviews: </span>{{ tvProps.vote_average }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Main",
  props: ["moviesProps", "tvProps"],
  data() {
    return {
      imageURL: "https://image.tmdb.org/t/p/w300",
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/styles/mixin.scss";
@import "@/styles/general.scss";
@import "@/styles/vars.scss";
.main-container {
  margin: 0 auto;
}
.cards-movie,
.cards-tv {
  min-height: 330px;
  width: 245px;
  border-radius: 6px;
  background-color: lightgray;
  margin: 18px;
  padding: 5px;
  float: left;
  text-align: start;
  &:hover {
    cursor: pointer;
  }
  span {
    font-size: 80%;
    color: gray;
    margin: 0 5px;
  }
  img {
    width: 30px;
    height: 20px;
    object-fit: contain;
  }
}
</style>
