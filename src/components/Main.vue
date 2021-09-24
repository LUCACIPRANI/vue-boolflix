<template>
  <!-- RICEVO !! 
    FIGLIO/ PADRE, da APP.VUE 
    passo PROPS 
-->
<div class="main-container">
  <div class="card-movie">
    <h4> <span >Title</span> {{ moviesProps.title }}</h4>
    <h4> <span >Original Title: </span> {{ moviesProps.original_title }}</h4>
    <div> <span >Language: </span> 
      <img :src="require(`../assets/img/${ moviesProps.original_language}.png`)">
    </div>
    <div> <span> Reviews: </span>{{ moviesProps.vote_average }}</div>
    <div> <span> images </span>{{ moviesProps.vote_average }}</div>

  </div>
</div>
</template>

<script>
export default {
  name: "Main",
  props: ["moviesProps"],
  data() {
    return {};
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/styles/mixin.scss";
@import "@/styles/general.scss";
@import "@/styles/vars.scss";
.main-container{
  margin: 0 auto;
}
.card-movie {
  min-height: 330px;
  width: 245px;
  border-radius: 6px;
  background-color: lightgray;
  margin: 18px;
  padding: 5px;
  float: left;
  text-align: start;
  &:hover{
    cursor: pointer;
  }
  span{
    font-size: 80%;
    color: gray;
    margin: 0 5px;
  }
  img{
    width: 30px;
    height: 20px;
    object-fit: contain;

  }
}
</style>
