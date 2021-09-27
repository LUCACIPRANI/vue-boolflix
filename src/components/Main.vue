<template>
  <div class="main-container">
    <!-- movies  -->
    <div class="cards">
      <div class="thefront">
        <img class="image" :src="`${imageURL}${info.poster_path}`" alt="" />
      </div>
      <div class="theback">
        <ul>
          <li>
            <span class="descr">Title: </span>
            {{ info ? info.name : info.title }}
          </li>
          <li>
            <span class="descr">Original Title: </span>
            {{ info ? info.original_title : info.original_name }}
          </li>
          <li>
            <span class="descr">Language: </span>
            <img
              class="flags"
              :src="require(`../assets/img/${info.original_language}.png`)"
            />
          </li>
          <li>
            <ul class="rating-list">
              <span class="descr"> Reviews: </span>
              <li><i class="fa fa-star yellow"></i></li>
              <li><i class="fa fa-star gray"></i></li>
              {{
                info.vote_average
              }}
            </ul>
          </li>
          <li>
            <span class="descr">Overview: </span>Lorem ipsum dolor sit amet
            consectetur adipisicing elit. Provident corrupti incidunt nulla
            necessitatibus autem rem fuga a, nobis, vitae consequuntur odio
            impedit est libero sequi officiis? Ad ipsum facere excepturi!
          </li>
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
    getRatings() {
      let ratings = this.info.vote_average;
      for (let rating in ratings) {
        const starProportion = Math.round(ratings[rating] / 2);
        console.log(starProportion);
      }
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
  margin: 0 auto;
  width: 92%;
}
.cards {
  position: relative;
  min-height: 380px;
  width: 220px;
  margin: 20px;
  border-radius: 6px;
  background-color: black;
  color: $color;
  line-height: 1.4rem;
  float: left;
  text-align: start;
  transform-style: preserve-3d;
  transition: all 2s ease;
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
  padding: 3px;
  .image {
    @include HeWi100();
    object-fit: cover;
  }
}
.theback {
  width: 100%;
  height: 100%;
  padding: 2px;
  backface-visibility: hidden;
  transform: rotateY(180deg);
  &:hover {
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
.fa-star:before {
  content: "\f005 \f005 \f005 \f005 \f005";
}
.rating-list li i.yellow {
  display: inline;
  color: #ffd700;
}
.rating-list li i.gray {
  display: none;
  color: gray;
}
.fa {
  display: inline-block;
}
</style>
