<template>
  <header>
    <div class="header">
      <h3 
        class="reset" 
        @click.prevent="reloadPage">
          <img src="https://analyticsindiamag.com/wp-content/uploads/2020/03/493f5bba-81a4-11e9-bf79-066b49664af6_cm_1440w.png" alt="">
      </h3>
      <div>
        <input
          @keyup.enter="$emit('performSearch', queryText)"
          type="text"
          placeholder="Type here"
          class="form-control"
          v-model="queryText"
        />
        <button @click.prevent="$emit('performSearch', queryText)" type="submit">
          Search
        </button>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      queryText: "",
    };
  },
  methods: {
    reloadPage() {
      this.queryText = "";
      this.$emit("searchMovie", this.queryText);
      location.reload();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "@/styles/mixin.scss";
@import "@/styles/general.scss";
@import "@/styles/vars.scss";

header {
  width: 100%;
  background-color: black;
  .header {
    @include spBetw();
    img{
      height: 60px;
      width: 120px;
    }
    h3 {
      color: $primarycolor;
      &:hover {
        cursor: pointer;
      };
    }
    input {
      padding: 8px;
      border: none;
    }
    button {
      background-color: $primarycolor;
      border: none;
      color: $color;
      padding: 8px;
      margin-right: 15px;
      font-weight: 700;
      &:hover {
        cursor: pointer;
        transform: scale(1.1);
      }
    }
  }
}
</style>
