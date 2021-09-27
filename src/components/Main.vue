<template>
  <div class="main-container">
    <!-- movies  -->
    <div class="cards">
      <div class="thefront">
        <img
          class="image"
          :src="`${imageURL}${info.poster_path}`"
          alt=""
        />
      </div>
      <div class="theback">
        <ul>
          <li> <span class="descr">Title: </span>  {{ (prova) ? info.name : info.title }}</li>
          <li><span class="descr">Original Title: </span>  {{ (prova) ? info.original_title : info.original_name }}</li>
          <li>
            <span class="descr">Language: </span> 
            <img 
              class="flags"
              :src="require(`../assets/img/${info.original_language}.png`)"
            />
          </li>
          <li><span class="descr"> Reviews: </span>{{ info.vote_average }}</li>
          <li><span class="descr">Overview: </span>Lorem ipsum dolor sit amet consectetur adipisicing elit. Provident corrupti incidunt nulla necessitatibus autem rem fuga a, nobis, vitae consequuntur odio impedit est libero sequi officiis? Ad ipsum facere excepturi!</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Main",
  props: ["info"],
  data() {
    return {
      imageURL: "https://image.tmdb.org/t/p/w342/",
    };
  },
  methods: {
    stars() {},
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
.cards{
  position: relative;
  min-height: 350px;
  width: 245px;
  margin: 20px;
  border-radius: 6px;
  background-color: black;
  color: white;
  line-height: 1.4rem;
  float: left;
  text-align: start;
  transform-style: preserve-3d;
  transition: all 2s ease;
  &:hover{
    transform: rotateY(180deg);
    cursor: pointer;
  }
}
.descr{
  font-weight: 700;
}
.thefront{
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  padding: 3px;
  .image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  }
}
.theback{
  width: 100%;
  height: 100%;
  padding: 2px;
  backface-visibility: hidden;
  transform: rotateY(180deg);
  &:hover{
    backface-visibility: visible;
  }
  ul li {
  list-style: none;
  }
  .flags {
    width: 30px;
    height: 20px;
    object-fit: cover;
  }
}

</style>
