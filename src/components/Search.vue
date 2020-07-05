<template>
  <div class="menu-1">
    <div class="flex-container-1">
      <div>
        <img src="../assets/himmel.png" ref="temp" width="35px" height="35px" />
      </div>
      <div>
        <label>Alles rund ums Wetter</label>
      </div>
      <div>
        <input
          type="text"
          v-model="cityName"
          name="newCityName"
          id="newCityName"
          placeholder="Ort"
          @keydown.enter="setLocation(); getWeatherCurrent(); showWeatherCurrent();"
        />
      </div>
    </div>
    <div class="flex-container-2">
      <div>
        <button
          type="submit"
          name="buttonCurrent"
          @mousedown="setLocation(); getWeatherCurrent(); showWeatherCurrent();"
        >Wetter Aktuell</button>
      </div>
      <div>
        <button
          type="submit"
          name="buttonForecast"
          @mousedown="setLocation(); getWeatherForecast(); showWeatherForecast();"
        >Wetter Vorhersage</button>
      </div>
      <div>
        <button
          type="submit"
          name="buttonUVIndex"
          @mousedown="setLocation(); getUVIndex(); showUVIndex();"
        >UV-Index</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      cityName: ""
    };
  },
  methods: {
    getWeatherCurrent() {
      this.$emit("get-weather-current");
    },
    getWeatherForecast() {
      this.$emit("get-forecast");
    },
    getUVIndex() {
      this.$emit("get-uv-index");
    },
    showWeatherCurrent() {
      this.$emit("show-weather-current");
    },
    showWeatherForecast() {
      this.$emit("show-weather-forecast");
    },
    showUVIndex() {
      this.$emit("show-uv-index");
    },
    setLocation() {
      if (this.cityName != "") {
        this.$emit("set-location", this.cityName);
      }
    }
  }
};
</script>

<style scoped>
.menu-1 {
  background: #4a6182;
  border-radius: 15px;
  margin: auto;
  margin-bottom: 10px;
  width: 40%;
  min-width: 500px;
  transition: all 0.5s ease-in-out;
  border: 4px solid#4a6182;
  
}
.flex-container-1 {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  align-content: center;
  padding-top: 15px;
  margin-top: 5px;
}
.flex-container-1 > div {
  margin-left: 10px;
  margin-right: 10px;
  text-align: center;
  line-height: 20px;
}
.flex-container-1 label {
  color: #f7f7ff;
  font-size: 23px;
  font-weight: bold;
  text-align: center;
}
.flex-container-1 input[type="text"] {
  padding: 12px 25px;
  border: none;
  cursor: pointer;
  outline: none;
  border-radius: 15px;
  color: #fe5f55;
  font-weight: bold;
  background: #f7f7ff;
}

.flex-container-2 {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  align-content: center;
  padding-top: 15px;
  padding-bottom: 15px;
  margin-bottom: 5px;
}
.flex-container-2 > div {
  margin-left: 10px;
  margin-right: 10px;
  text-align: center;
  line-height: 20px;
}
.flex-container-2 button {
  color: #f7f7ff;
  background-color: #fe5f55;
  font-weight: bold;
  border-radius: 15px;
  padding: 12px 25px;
  border: none;
  cursor: pointer;
  outline: none;
}
.flex-container-2 button:hover {
  color: #fe5f55;
  background-color: #f7f7ff;
  padding: 12px 25px;
  transition: 0.65s;
}
::placeholder {
  color: #fe5f55;
}
@media only screen and (max-width: 1024px) {
  .menu-1 {
    width: 90%;
  }
}
</style>
