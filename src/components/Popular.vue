<template>
  <div class="main-container">
    <h1>Popular on NETFLIX</h1>
    <div class="cards">
      <div class="thefront">
        <p v-if="info.poster_path">
          <img
            class="image"
            :src="`${imageURL}${info.poster_path}`"
            :alt="info.name"
          />
        </p>
        <p v-else>
          <img
            class="noImage"
            src="../assets/img/no-av.jpeg"
            :alt="info.name"
          />
        </p>
      </div>
      <div class="theback">
        <ul>
          <li>
            <span class="descr">name: </span>
            {{ info.name }}
          </li>
          <li>
            <span class="descr">Popularity: </span>
            <i>{{ info.popularity}}</i>
          </li>
          <li>
            <span class="descr">Overview: 
            <p>
              {{info.overview}}
            </p>
            </span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Popular",
  props: ["info"],
  data() {
    return {
      imageURL: "https://image.tmdb.org/t/p/w342/",
    };
  },
  methods: {
    getVote() {
      return Math.ceil(this.info.vote_average / 2);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/styles/mixin.scss";
@import "@/styles/general.scss";
@import "@/styles/vars.scss";

.main-container {
  margin: 60px auto;
  margin-bottom: 30px;
  width: 93%;
}
.cards {
  position: relative;
  @include cardSize();
  background-color: black;
  color: $color;
  line-height: 1.4rem;
  float: left;
  text-align: start;
  transform-style: preserve-3d;
  transition: transform 2s;
  &:hover {
    transform: rotateY(180deg);
    cursor: pointer;
  }
  .descr {
    font-weight: 700;
  }
}
.thefront {
  position: absolute;
  @include HeWi100();
  backface-visibility: hidden;
  color: $color;
  .image {
    @include HeWi100();
    object-fit: contain;
  }
  .noImage {
    @include cardSize();
  }
}
.theback {
  position: absolute;
  @include HeWi100();
  padding: 2px;
  backface-visibility: hidden;
  transform: rotateY(180deg);
  color: $color;
  ul{
    backface-visibility: hidden;
  }
  ul li {
    list-style: none;
  }
  p{
  display: inline;
  font-size: 80%;
  font-weight: 300;
  }
}
</style>
