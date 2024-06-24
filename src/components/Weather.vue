<template>
  <div class="weather-widget">
    <h2>Weather Widget</h2>
    <p style="color: white">Enter a city name to see the weather.</p>
    <div class="search-bar">
      <input v-model="city" placeholder="Enter city name" @keyup.enter="getWeather" />
      <button @click="getWeather">Search</button>
    </div>
    <div v-if="weather" class="weather-info">
      <div class="weather-item">
        <p class="bold-text"><strong>Location:</strong> {{ weather.name }}</p>
        <p class="bold-text"><strong>Weather:</strong> {{ weather.weather[0].description }} </p>
        <p class="bold-text"><strong>Humidity:</strong> {{ weather.main.humidity }}%</p>
        <p class="bold-text"><strong>Temperature:</strong> {{ weather.main.temp }}°C</p>
      </div>
    </div>
    <div v-else>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const city = ref('')
const weather = ref(null)

const getWeather = async () => {
  const apiKey = 'ceb97d9ca273e7696ff7f99b1a1fa728'
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&units=metric&appid=${apiKey}`

  try {
    const response = await axios.get(url)
    weather.value = response.data
  } catch (error) {
    console.error(error)
    weather.value = null
  }
}
</script>

<style scoped>

.body{
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.weather-widget {
  padding: 20px;
  border-radius: 10px;
  max-width: 700px;
  margin: 200px auto 50px auto;
  text-align: center;
  background-color:burlywood;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.weather-widget h2 {
  color:white;
  font-size: 36px;
  font-weight: bold;
  margin-bottom: 20px;
}

.search-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
  border: 2px solid white;
  background-color: white;
}

.search-bar input {
  padding: 10px;
  width: 90%;
  margin-right: 10px;
  border-radius: 5px;
  color: rgb(0, 0, 0);
}

.search-bar button {
  padding: 10px;
  border:white;
  background-color:white;
  color: burlywood;
  cursor: pointer;
}

.weather-info {
  margin-top: 20px; 
  display: flex;
  justify-content: center; 
  align-items: center;
  flex-wrap: wrap; 
}

.weather-item {
  border-radius: 5px;
  padding: 100px;
  color: black;
  text-align: center;
  font-size: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.weather-item img {
  margin-top: 10px;
  width: 35px;
  height: 35px;
}

.weather-item p {
  margin: 0;
  color: black;
  font-weight: bold; /* Made text bold */
}

.weather-border {
  margin-top: 10px;
  padding-top: 10px;
}

.bold-text {
  font-weight: bold;
  color: black;
}

</style>
