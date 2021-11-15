<template>
<Loader v-if="!forecast"></Loader >
<div class="container" v-if="forecast">
    <div class="my-container">
        <div class=" row">
            <div class="col border border-primary text-primary mt-3">
                    <div class="text-center mt-2 mb-2">
                        <span>Maribor coords: </span>
                        <button @click="MariborDefaultCoordinates()" class="btn btn-sm btn-primary text-warning bg-primary">Get Coords</button>
                    </div>
                    <div class="form-row form-inline d-flex justify-content-center mt-2 mb-2">
                        <label for="lat">Lat:</label>
                        <input type="text" class="form-control col-sm-2 border-primary" id="lat" v-model="lat" placeholder="Enter lat">
                        <label for="lon">Lon:</label>
                        <input type="text" class="form-control border-primary col-sm-2" id="lon" v-model="lon" placeholder="Enter lon">
                    </div>
                    <div class="text-center">
                        <button @click="getUserLocation()" class="btn btn-primary btn-sm bg-primary text-warning">Get my current location</button>
                        <p><b>Timezone: </b>{{forecast.timezone}}</p>
                        <!-- <p class="text-center">Coordinates: lat: {{forecast.lat}} , lon: {{forecast.lon}}</p>                 -->
                    </div>
                    <div>
                        <div class="text-center">
                            <button @click="updateForecast()" class="btn btn-primary bg-primary text-warning">Update Forecast</button>
                        </div>
                        <div>
                            <p class="text-center"><span><b>Obtained on:</b> </span> {{getDateMethod().toLocaleString()}}</p>
                        </div>
                    </div>
            </div>
        </div>
        <div class="row border border-primary mt-1 text-primary">
            <div class="col-md-6 col-sm-12 mb-1 mt-1">
              <div>
                  <h5>
                        <p class="text-center "><b>Timezone: </b>{{forecast.timezone}}</p>
                  </h5>
                  <div>
                      <p class="text-center"><span>{{getDateMethod().toDateString()}}</span></p>
                  </div>
                  <div>
                    <h3 class="text-center">Current temp: {{forecast.current.temp}} °</h3>
                  </div>
                  <div class="text-center p-">
                    <!-- <img src="http://openweathermap.org/img/wn/04d@2x.png"> -->
                    <img style="width:100px; height:100px" :src="'http://openweathermap.org/img/w/' + forecast.current.weather[0].icon + '.png' ">
                  </div>
                  <div>
                    <p class="text-center"><b>Description:</b> {{forecast.current.weather[0].main}}, {{forecast.current.weather[0].description}}.</p>
                  </div>
                  <div class="text-center">
                    <p><b>Feels like: </b>{{forecast.current.feels_like}} ° </p>
                    <p><b>Pressure: </b>{{forecast.current.pressure}} hPa </p>
                    <p><b>Humidity: </b>{{forecast.current.humidity}} % </p>
                  </div>
              </div>
            </div>
            <div class="col-md-6 col-sm-12">
                <div v-for="index in 5" :key="index" class="row border border-primary">
                    <div class="col">
                        <p class="text-center p-1">{{new Date((forecast.daily[index-1].dt * 1000)).toDateString()}}</p>
                    </div>
                    <div class="col">
                        <span><img style="width:80px; height:80px" :src="'http://openweathermap.org/img/w/' + forecast.daily[index-1].weather[0].icon + '.png' "/></span>
                    </div>
                    <div class="col">
                        <p class="m-1">
                            <span>Min: {{Math.round(forecast.daily[index-1].temp.min)}} ° </span>
                        </p>
                        <p>
                            <span>Max: {{Math.round(forecast.daily[index-1].temp.max)}} °  </span>
                        </p>
                    </div>
                    <div class="col">
                        <p><b>Description:</b> {{forecast.daily[index-1].weather[0].main}} </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>


</template>

<script>
import Loader from "./Loader.vue"

export default {
    name:"WeatherComponent",
    data(){
        return {
            api_key: "7ca6e152197750c5f2ed06aa6d6c687c",
            forecast: null,
            lat:"46.55",
            lon:"15.64"
        }
    },
    //getting the data from API and saving it to forecast in data()
    methods: {
        getForecast(){
            fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=${this.lat}&lon=${this.lon}&units=metric&exclude=hourly,minutely&appid=${this.api_key}`)
            .then(res => res.json())
            .then(data=>
            this.forecast=data);
        },
        updateForecast(){
            this.getForecast();
        },
        getDateMethod(){
            return new Date();
        },
        MariborDefaultCoordinates(){
            this.lat="46.55",
            this.lon="15.64"
        },
        getUserLocation(){
            var currObj = this;
            if (navigator.geolocation){
                navigator.geolocation.getCurrentPosition(function(position){
                currObj.lat = position.coords.latitude;
                currObj.lon = position.coords.longitude;
                })
            } 
            else alert("Geolocation is not supported by this browser");
        },
    },
    components: {
        Loader
    },
    computed:{

    },
    created(){
    //setTimeout just to be able to see the loader longer, otherwise just this.getForecast();
    setTimeout(() => {
        this.getForecast();
        }, 500);
    },
    
}
</script>

<style scoped>
* {
    background-color:#b2cced;
}
.my-container{
padding:11%;
}


</style>