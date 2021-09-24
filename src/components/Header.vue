<template>
  <!--INVIO !!
    FIGLIO/ PADRE, con HEADER-- APP.VUE 
    passo EMIT 
-->
  <header>
    <div class="header">
      <h4>BOOLFLIX</h4>
      <div>
        <input type="text" class="form-control" v-model="queryText" />
        <button @click="$emit('search', 'queryText')" type="submit">
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
  mounted() {},
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
    padding: 10px;
    h4 {
      color: $primarycolor;
    }
    input {
      margin: 0 5px;
      padding: 2px;
      &:hover {
        cursor: pointer;
      }
    }
    button {
      background-color: white;
      border: none;
      padding: 3.5px;
      font-weight: 700;
      &:hover {
        cursor: pointer;
        transform: scale(1.1);
      }
    }
  }
}
</style>
