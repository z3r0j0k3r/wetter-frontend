<template>
  <div id="app">
    <div id="wrapper">
      <Search
        v-on:get-weather-current="getWeatherCurrent"
        v-on:get-forecast="getWeatherForecast"
        v-on:get-uv-index="getUVIndex"
        v-on:show-weather-current="showWeatherCurrent"
        v-on:show-weather-forecast="showWeatherForecast"
        v-on:show-uv-index="showUVIndex"
        v-on:set-location="setLocation"
      ></Search>
      <Current
        v-if="show.weatherCurrent && !loading"
        v-bind:weatherDataCurrent="weatherDataCurrent"
      ></Current>
      <Forecast
        v-if="show.weatherForecast && !loading"
        v-bind:weatherDataForecast="weatherDataForecast"
      ></Forecast>
      <UV v-if="show.uvIndex && !loading" v-bind:uvData="uvData"></UV>
    </div>
  </div>
</template>

<script>
import axios from "axios";

import Search from "./components/Search";
import Current from "./components/Current";
import Forecast from "./components/Forecast";
import UV from "./components/UV";

export default {
  name: "App",
  components: {
    Search,
    Current,
    Forecast,
    UV
  },

  data() {
    return {
      cityName: "",

      exampleCitys: [
        "Berlin",
        "New York",
        "Paris",
        "Prag",
        "Moskau",
        "Male",
        "Bangkok",
        "Tokyo",
        "Hawaii",
        "Los Angeles",
        "Kapstadt",
        "Stockholm",
        "Zurich",
        "Washington DC"
      ],

      weatherDataCurrent: [],
      weatherDataForecast: [],
      uvData: [],

      longitude: 0,
      latitude: 0,

      apiKey: "5c70cb6c1bf42d9dadd493558eb7ba68",
      units: "metric",

      show: {
        weatherCurrent: false,
        weatherForecast: false,
        uvIndex: false
      },

      loading: false
    };
  },
  methods: {
    async getWeatherCurrent() {
      this.loading = true;
      try {
        const response = await axios.get(
          "http://api.openweathermap.org/data/2.5/weather?q=" +
            this.cityName +
            "&appid=" +
            this.apiKey +
            "&units=" +
            this.units +
            "&lang=de"
        );
        this.weatherDataCurrent = response.data;
      } catch (e) {
        console.log(e);
      } finally {
        this.loading = false;
      }
    },

    async getWeatherForecast() {
      this.loading = true;
      try {
        const response = await axios.get(
          "http://api.openweathermap.org/data/2.5/forecast?q=" +
            this.cityName +
            "&appid=" +
            this.apiKey +
            "&units=" +
            this.units
        );
        this.weatherDataForecast = response.data;
      } catch (e) {
        console.log(e);
      } finally {
        this.loading = false;
      }
    },

    async getUVIndex() {
      this.loading = true;
      await this.getWeatherCurrent();
      this.setCoordinates();
      try {
        const response = await axios.get(
          "http://api.openweathermap.org/data/2.5/uvi?appid=" +
            this.apiKey +
            "&lat=" +
            this.latitude +
            "&lon=" +
            this.longitude
        );
        this.uvData = response.data;
      } catch (e) {
        console.log(e);
      } finally {
        this.loading = false;
      }
    },
    setLocation(cityName) {
      this.cityName = cityName;
    },
    setCoordinates() {
      this.longitude = this.weatherDataCurrent.coord.lon;
      this.latitude = this.weatherDataCurrent.coord.lat;
    },
    showWeatherCurrent() {
      this.show.weatherCurrent = true;
      this.show.weatherForecast = false;
      this.show.uvIndex = false;
    },
    showWeatherForecast() {
      this.show.weatherCurrent = false;
      this.show.weatherForecast = true;
      this.show.uvIndex = false;
    },
    showUVIndex() {
      this.show.weatherCurrent = false;
      this.show.weatherForecast = false;
      this.show.uvIndex = true;
    }
  },
  mounted() {
    this.setLocation(
      this.exampleCitys[Math.floor(Math.random() * Math.floor(14))]
    );
    this.getWeatherCurrent();
    this.showWeatherCurrent();
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
