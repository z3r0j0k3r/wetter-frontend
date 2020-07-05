<template>
  <div class="box">
    <div id="forecast" class="center">
      <ul>
        <li v-for="singleForecast in filteredWeatherDataForecast" :key="singleForecast.id">
          <h6>{{tmp = getImgStringForecast(singleForecast.weather[0].icon)}}</h6>
          <img :src="tmp" />
          <ul>
            <li class="text-center">{{getDateString(singleForecast.dt_txt)}}</li>
            <li>
              <span class="large">{{Math.round(singleForecast.main.temp)}}C°</span>
              <div class="text-right">
                <div class="min">Min: {{Math.round(singleForecast.main.temp_min)}}C°</div>
                <div class="max">Max: {{Math.round(singleForecast.main.temp_max)}}C°</div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "Forecast",
  props: ["weatherDataForecast"],
  methods: {
    getImgStringForecast(imgStringForecast) {
      this.imgStringForecast =
        "http://openweathermap.org/img/wn/" + imgStringForecast + "@2x.png";
      return this.imgStringForecast;
    },
    getDateString(strDate) {
      //https://developer.mozilla.org/de/docs/Web/JavaScript/Reference/Global_Objects/Date/toLocaleString
      var t = strDate.split(/[- :]/);
      var d = new Date(t[0], t[1] - 1, t[2], t[3], t[4], t[5]);
      var options = {
        weekday: "short",
        //year: "2-digit",
        month: "short",
        day: "numeric"
      };
      return d.toLocaleString("de-DE", options);
    }
  },
  computed: {
    filteredWeatherDataForecast: function() {
      return this.weatherDataForecast.list.filter(function(value, index) {
        if (index > 0) return index % 7 == 0;
      });
    }
  }
};
</script>

<style scoped>
h6 {
  display: none;
}

.text-right {
  float: right;
}

.text-center {
  text-align: center;
}

.large {
  font-size: 1.8em;
  padding-left: 2px;
}
.min,
.max {
  font-size: 0.8em;
}
.box {
  width: 42%;
  margin: auto;
  min-width: 500px;
}
#forecast {
  display: inline-flex;
  text-align: center;
  transition: all 0.5s ease-in-out;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

ul > li {
  float: none;
  text-align: left;
  padding-bottom: 10px;
}

#forecast > ul {
  padding: 3px;
}

#forecast > ul > li {
  background: #cce9ff;
  color: #4a6182;
  width: 30%;
  margin: 4px;
  text-align: right;
  display: inline-block;
  border-radius: 5%;
  font-size: 120%;
  border: 4px solid#4a6182;
}

ul li a {
  padding-top: 20%;
}

ul li img {
  display: block;
  margin: auto;
}

/* responsive definition */
@media only screen and (max-width: 1024px) {
  #forecast > ul {
    width: 100%;
  }
  .box {
    text-align: center;
    width: 90%;
  }
  #forecast > ul > li {
    width: 30%;
    float: none;
  }
}

@media only screen and (max-width: 768px) {
  #forecast > ul {
    width: 100%;
  }
  #forecast > ul > li {
    width: 45%;
    float: none;
  }
}
@media only screen and (max-width: 468px) {
  #forecast > ul {
    width: 100%;
  }
  #forecast > ul > li {
    width: 90%;
    float: none;
  }
}
</style>