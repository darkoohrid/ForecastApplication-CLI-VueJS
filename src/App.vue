<template >
  <Header></Header>
  <WeatherComponent></WeatherComponent>

</template>

<script>
import Header from "./components/Header.vue";
import WeatherComponent from "./components/WeatherComponent.vue";

export default {
  components: {
    Header,
    WeatherComponent   
  }
};
</script>

<style scoped>
body{
  background-color:rgb(245, 238, 238);
}
</style>
