<template>
  <div id="current">
    <div class="text-box">
      <div
        class="text-center"
      >{{this.weatherDataCurrent.name}}, {{this.weatherDataCurrent.sys.country}}</div>

      <div class="icon-big">
        {{this.getTmpImgString()}}
        <img :src="this.imgString" alt="WeatherICO" />
      </div>

      <div class="text-temp">
        <img src="../assets/TemperaturIcon.png" ref="temp" width="9%" height="9%" />
        {{Math.round(this.weatherDataCurrent.main.temp)}}°c
      </div>

      <div class="text-right">
        Min: {{Math.round(this.weatherDataCurrent.main.temp_min)}}°c
        <br />
        Max: {{Math.round(this.weatherDataCurrent.main.temp_max)}}°c
      </div>
      <div class="last-line-box">
        <div class="last-line">
          <div class="text-left">{{this.weatherDataCurrent.weather[0].main}}</div>

          <div class="text-right-additional">
            <img src="../assets/WindIcon.png" ref="temp" width="5%" height="5%" />
            {{Math.round(this.weatherDataCurrent.wind.speed)}}km/h
            <img
              src="../assets/water-48.png"
              ref="temp"
              width="25px"
              height="25px"
            />
            {{Math.round(this.weatherDataCurrent.main.humidity)}}%
          </div>
        </div>
      </div>

      <div
        class="center"
      >{{this.weatherDataCurrent.weather[0].description}} in {{this.weatherDataCurrent.name}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Current",
  props: ["weatherDataCurrent"],
  data() {
    return {
      tmpImgString: "",
      imgString: ""
    };
  },
  methods: {
    getTmpImgString() {
      this.tmpImgString = this.weatherDataCurrent.weather[0].icon;
      this.imgString =
        "http://openweathermap.org/img/wn/" + this.tmpImgString + "@4x.png";
    }
  }
};
</script>

<style scoped>
#current {
  background: #cce9ff;
  color: #4a6182;
  width: 40%;
  height: 225px;
  margin: auto;
  padding-bottom: 20px;
  margin-bottom: 20px;
  transition: all 0.5s ease-in-out;
  border-radius: 25px;
  font-size: 16px;
  min-width: 500px;
  border: 4px solid#4a6182;
}
.text-center {
  text-align: center;
  font-size: 30px;
  font-weight: bold;
  padding-top: 10px;
}
.text-box {
  display: inline-block;
}
.icon-big {
  margin-top: -30px;
}
.text-temp {
  margin-top: -125px;
  font-size: 46px;
  font-weight: bold;
  text-align: center;
}
.text-temp img {
  vertical-align: middle;
}
.last-line-box {
  margin-top: 100px;
}
.last-line {
  display: table-row;
}

.text-left {
  font-weight: bold;
  text-align: left;
  padding-left: 52px;
  font-size: 26px;
  display: table-cell;
  letter-spacing: 1px;
}

.text-right {
  font-weight: bold;
  text-align: right;
  margin-top: -110px;
  letter-spacing: 1px;
  padding-right: 20px;
}

.text-right-additional {
  font-weight: bold;
  display: table-cell;
  text-align: right;
  padding-right: 20px;
  letter-spacing: 1px;
  margin-top:-200px;
}
.text-right-additional img {
  vertical-align: bottom;
}

.center {
  text-align: center;
  font-weight: bold;
  visibility: hidden;
  margin-top: 12px;
}

#current:hover {
  font-size: 1.5em;
  transition: all 0.5s ease-in-out;
  height: 2%;
}
#current:hover .center {
  visibility: visible;
}
#current:hover .text-temp {
  font-size: 2.5em;
}
#current:hover .text-left {
  font-size: 1.5em;
}

form {
  display: block;
  text-align: center;
  margin-bottom: 10px;
}
/* responsive definition */
@media only screen and (max-width: 1024px) {
  #current {
    width: 90%;
  }
}
@media only screen and (max-width: 550px) {
  .text-temp {
    text-align: right;
    padding-right: 120px;
  }
}
</style>