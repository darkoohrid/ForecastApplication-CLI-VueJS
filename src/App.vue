<template>
  <Header></Header>
  <WeatherComponent v-if="isDataLoaded"></WeatherComponent>
  <Loader v-else></Loader>
</template>

<script>
import Header from "./components/Header.vue";
import WeatherComponent from "./components/WeatherComponent.vue";
import Loader from "./components/Loader.vue"

export default {
  name:"app",
  data(){
    return {
      isDataLoaded:false,
      forecast:{}
    }
  },
  methods:{
    getForecast(){
      fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=46.55&lon=15.64&units=metric&exclude=hourly,minutely&appid=7ca6e152197750c5f2ed06aa6d6c687c`)
      .then(res => res.json())
      .then(data=>
      this.forecast=data); 
      }    
  },
  components: {
    Header,
    WeatherComponent,
    Loader   
  },
  created(){
    this.isDataLoaded = false;
    setTimeout(() => {
      this.getForecast();
      this.isDataLoaded = true;
      console.log("here");
    }, 1000);
  }
};
</script>

<style>
body {
    background-color: rgb(50, 107, 192)
  }
</style>
