<template>
<div class="container">
    <div class="my-container">
        <div class=" row my-row">
            <div class="col my-col">
                    <div>
                        <p class="text-center"><b>Timezone: </b>{{forecast.timezone}}</p>
                        <!-- <p class="text-center">Coordinates: lat: {{forecast.lat}} , lon: {{forecast.lon}}</p>                 -->                 
                    </div>
                    <div class="text-center">
                        <button @click="getForecast()" class="btn btn-primary">Update Forecast info</button>
                    </div>
                    <div>                    
                        <p class="text-center"><span><b>Obtained on:</b> </span> {{getDateMethod().toLocaleString()}}</p>
                    </div>
            </div>
        </div>
        <div class="row my-row mt-1">
            <div class="col-md-6 col-sm-12 my-col mb-1 mt-1">
              <div>
                  <div>
                      <h3>Maribor, Sl</h3>
                      <p><span>{{getDateMethod().toDateString()}}</span></p>
                  </div>
                  <div>
                    <h3 class="text-center">Current temp: {{forecast.current.temp}} °</h3>
                  </div>
                  <div class="text-center">
                    <!-- <img src="http://openweathermap.org/img/wn/04d@2x.png"> -->
                    <img :src="'http://openweathermap.org/img/w/' + forecast.current.weather[0].icon + '.png' ">
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
            <div class="col-md-6 col-sm-12 my-col mb-1 mt-1">
                <div v-for="index in 5" :key="index" class="row border">
                    <div class="col">
                        <p class="text-center">{{(getDateMethod(forecast.daily[index-1].dt * 1000)).toDateString()}}</p>
                    </div>
                    <div class="col">
                        <span><img style="width:80px; height:80px" :src="'http://openweathermap.org/img/w/' + forecast.daily[index-1].weather[0].icon + '.png' "/></span>                       
                    </div>
                    <div class="col">
                        <p>
                            <span>Min:{{Math.round(forecast.daily[index-1].temp.min)}} ° </span> 
                        </p>
                        <p class="">
                            <span>Max:{{Math.round(forecast.daily[index-1].temp.max)}} °  </span>  
                        </p>
  
                    </div>
                    <div class="col">
                        <p class=""><b>Description:</b> {{forecast.daily[index-1].weather[0].main}} </p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>  


</template>

<script>
export default {
    name:"WeatherComponent",
    data(){
        return {
            api_key: "7ca6e152197750c5f2ed06aa6d6c687c",
            forecast: {}
        }
    },
    methods: {
        getForecast(){
            fetch(`https://api.openweathermap.org/data/2.5/onecall?lat=46.55&lon=15.64&units=metric&exclude=hourly,minutely&appid=7ca6e152197750c5f2ed06aa6d6c687c`)
            .then(res => res.json())
            .then(data=>
            this.forecast=data); 
        },
        getDateMethod(){
            return new Date();
        },
    },
    computed:{
        
    },
    created(){
        this.getForecast();
        console.log(this.forecast);
    }
}
</script>

<style scoped>
.my-container{
    margin:10%;
}
.my-row{
    border:3px solid red;
}
.my-col{
    border:3px dotted blue;
}

</style>