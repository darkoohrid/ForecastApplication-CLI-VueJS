<template>
  <Header></Header>
  <WeatherComponent></WeatherComponent>
</template>

<script>
import Header from "./components/Header.vue";
import WeatherComponent from "./components/WeatherComponent.vue";

export default {
  name:"app",
  components: {
    Header,
    WeatherComponent 
  }
};
</script>

<style>
body {
    background-color: rgb(50, 107, 192)
  }
</style>
