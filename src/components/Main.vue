<template>
  <div class="main-container">
    <!-- movies  -->
    <div class="cards">
      <div class="thefront">
        <p v-if="info.poster_path">
          <img
            class="image"
            :src="`${imageURL}${info.poster_path}`"
            :alt="info.name ? info.name : info.title"
          />
        </p>
        <p v-else>
          <img
            class="unAvail"
            src="../assets/img/no-av.jpeg"
            :alt="info.name ? info.name : info.title"
          />
        </p>
      </div>
      <div class="theback">
        <ul>
          <li>
            <span class="descr">Title: </span>
            {{ info.name ? info.name : info.title }}
          </li>
          <li>
            <span class="descr">Original Title: </span>
            {{ info.original_title ? info.original_title : info.original_name }}
          </li>
          <li>
            <span class="descr">Language: </span>
            <img
              v-if="availableFlags.includes(info.original_language)"
              class="flags"
              :src="require(`../assets/img/${info.original_language}.png`)"
            />
            <p v-else>{{ info.original_language }}</p>
          </li>
          <li>
            <span class="descr">Review: </span>
            <i
              v-for="n in 5"
              :key="n"
              class="fa-star"
              :class="n <= getVote() ? 'fas' : 'far'"
            >
            </i>
          </li>
          <li>
            <span class="descr">Overview: 
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Provident corrupti incidunt nulla necessitatibus autem rem fuga a, nobis, vitae consequuntur odio impedit est libero sequi officiis? Ad ipsum facere excepturi!
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
  name: "Main",
  props: ["info"],
  data() {
    return {
      imageURL: "https://image.tmdb.org/t/p/w342/",
      availableFlags: [
        "it",
        "cs",
        "en",
        "es",
        "ru",
        "de",
        "zh",
        "ja",
        "po",
        "fr",
      ],
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
  .unAvail {
    @include cardSize();
  }
}
.theback {
  @include HeWi100();
  padding: 2px;
  backface-visibility: hidden;
  transform: rotateY(180deg);
  color: $color;
  ul li {
    list-style: none;
  }
  p{
  display: inline;
  font-size: 80%;
  font-weight: 300;
  }
  .flags {
    width: 30px;
    height: 20px;
    object-fit: cover;
  }
  .fa-star {
    color: #ffd700;
  }
}
</style>
