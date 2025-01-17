<template>
    <div :style="cardStyle" class="weather-card">
      <h2>{{ city }}</h2>
      <p>Current temperature : {{ temperature }} °C</p>
      <p>Weather condition : {{ weatherDescription }}</p>
      <p>Wind speed : {{ windSpeed }} km/h</p>
      <p>Last update : {{ lastUpdated }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      city: String,
      temperature: Number,
      weatherDescription: String,
      windSpeed: Number,
      lastUpdated: String,
    },
    computed: {
      cardStyle() {
        if (this.temperature < 10) {
          return { backgroundColor: '#87CEEB', color: '#fff' };
        } else if (this.temperature <= 25) {
          return { backgroundColor: '#90EE90', color: '#000' };
        } else {
          return { backgroundColor: '#FF6347', color: '#fff' };
        }
      },
    },
  };
  </script>
  
  <style>
  .weather-card {
    padding: 20px;
    border-radius: 8px;
    margin: 20px 0;
    text-align: center;
  }
  </style>
  