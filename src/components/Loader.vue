<template>
  <div class="loader">
    <img src="../../public/logo-netflix.png" alt="" />
    <div class="text">Loading Boolflix...</div>
  </div>
</template>

<script>
export default {
  name: "Loader",
  props: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import "../styles/vars";

.loader {
  background-image: url(../assets/img/bg-netflix.jpeg);
  background-size: cover;
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background-color: $secondarycolor;
}
.text {
  color: white;
  font-size: 40%;
  margin-top: 100px;
  animation: animate 2s linear infinite;
}

img {
  width: 70px;
  margin: 1rem 0;
  animation: animate 2s linear infinite;
}

@keyframes animate {
  from{
    transform: scale(1.5) perspective(10px);
  }
  to{
    transform: scale(3.5) perspective(10px);
  }
}
</style>
