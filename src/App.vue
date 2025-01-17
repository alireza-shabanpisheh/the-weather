<template>
  <div class="all-section">
    <div id="app">
      <div class="header">
        <h1 class="title">Weather</h1>
        <div class="img_container">
          <img class="img-org" src="./assets/icons/partly-cloudy.png" alt="">
        </div>
      </div>
      <WeatherCard 
        v-if="weatherData"
        :city="weatherData.city"
        :temperature="weatherData.temperature"
        :weatherDescription="weatherData.description"
        :windSpeed="weatherData.windSpeed"
        :lastUpdated="weatherData.lastUpdated"
      />
      <div class="serachBox">
        <input 
          v-model="cityName" 
          placeholder="City Name"
          @keyup.enter="fetchWeather"
        />
        <button @click="fetchWeather" class="findBtn">Find City</button>
      </div>
      <p v-if="errorMessage" style="color: red;" class="error_msg">{{ errorMessage }}</p>

    </div>
  </div>
</template>

<script>

import WeatherCard from './components/WeatherCard.vue';


const cities = [
  {
    name: "Tehran",
    temperature: 30,
    description: "Sunny",
    windSpeed: 5.5,
    lastUpdate: "5 minutes ago",
  },
  {
    name: "Mashhad",
    temperature: 18,
    description: "Cloudy",
    windSpeed: 7.2,
    lastUpdate: "10 minutes ago",
  },
  {
    name: "Isfahan",
    temperature: 12,
    description: "Rainy",
    windSpeed: 6.3,
    lastUpdate: "8 minutes ago",
  },
  {
    name: "Tabriz",
    temperature: 8,
    description: "Snowy",
    windSpeed: 4.1,
    lastUpdate: "3 minutes ago",
  },
];

export default {
  components: { WeatherCard },
  data() {
    return {
      cityName: '',
      weatherData: null,
      errorMessage: '',
    };
  },
  methods: {
    fetchWeather() {
      
      const city = cities.find(
        (item) => item.name.toLowerCase() === this.cityName.toLowerCase()
      );

      if (city) {
        this.weatherData = {
          city: city.name,
          temperature: city.temperature,
          description: city.description,
          windSpeed: city.windSpeed,
          lastUpdated: city.lastUpdate,
        };
        this.errorMessage = '';
      } else {
        this.weatherData = null;
        this.errorMessage = 'City not found...';
      }
    },
  },
};
</script>

<style>
.error_msg {
  font-weight: bold;
  font-size: 32px;
}
.header {
  display: flex;
  gap: 165px;

}
.img_container{
  width: 50px;
  margin: auto;
  
}
.img-org{
  width: 100%;
  object-fit: cover;
}
.title {
  font-weight: bold;
}
body {
  background-color: #B3E5FC;
}
.all-section {
  border-radius: 15px;
  background-color: #F5F5F5;
  margin: 0 auto;
  width: 400px;
}
.findBtn{
  color: white;
  background-color: #3949AB;
  border-radius: 10px;
  padding-top: 10px;
  padding-bottom: 10px;
}
.serachBox {
  display: flex;
  flex-direction: column;
  gap: 25px;
}
#app {
  text-align: center;
  max-width: 600px;
  margin: auto;
  padding: 20px;
}
input {
  margin-right: 10px;
  padding: 5px;
}
button {
  padding: 5px 10px;
}
</style>
