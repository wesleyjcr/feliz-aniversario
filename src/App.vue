<template>
  <img alt="Vue logo" src="./assets/cake.svg" />
  <FelizAniversario />
</template>

<script>
  import FelizAniversario from "./components/FelizAniversario.vue";

  export default {
    name: "App",
    components: {
      FelizAniversario,
    },
  };
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  img {
    height: 200px;
  }
</style>
