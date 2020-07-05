<template>
  <div id="uv">
    <div class="text-center">UV-Index Heute</div>
    <div class="center-box">
      <table class="center">
        <div class="small-green">
          <h2>1-2</h2>
          <h3>Niedrig</h3>
        </div>
        <div class="small-yellow">
          <h2>3-5</h2>
          <h3>Mittel</h3>
        </div>
        <div class="small-orange">
          <h2>6-7</h2>
          <h3>Hoch</h3>
        </div>
        <div class="small-red">
          <h2>8-10</h2>
          <h3>Sehr Hoch</h3>
        </div>
        <div class="small-purple">
          <h2>10+</h2>
          <h3>Extrem Hoch</h3>
        </div>
      </table>
    </div>
    <div class="box-left">
      <div class="text-left">
        {{this.getUVColor(Math.round(uvData.value))}}
        <img
          src="https://img.icons8.com/dusk/64/000000/do-not-expose-to-sunlight.png"
          width="64px"
          height="64px"
        />
        {{Math.round(uvData.value)}}
        <a>uv</a>
      </div>
    </div>

    <div v-if="num == 0 && num <= 2" class="green">
      <h1>Niedrig</h1>
      <a>kein Schutz notwendig</a>
    </div>
    <div v-if="num >= 3 && num <= 5" class="yellow">
      <h1>Mittel</h1>
      <a>Schutz notwendig</a>
    </div>
    <div v-if="num >= 6 && num <= 7" class="orange">
      <h1>Hoch</h1>
      <a>Schutz notwendig</a>
    </div>
    <div v-if="num >= 8 && num <= 10" class="red">
      <h1>Sehr Hoch</h1>
      <a>Zusätzlicher Schutz notwendig</a>
    </div>
    <div v-if="num >= 11" class="purple">
      <h1>Extrem Hoch</h1>
      <a>Zusätzlicher Schutz notwendig</a>
    </div>
  </div>
</template>


<script>
export default {
  name: "UV",
  props: ["uvData"],

  data() {
    return {
      num: 0
    };
  },

  methods: {
    getUVColor(tmp) {
      this.num = tmp;
    }
  }
};
</script>


<style scoped>
#uv {
  background: #cce9ff;
  color: #4a6182;
  width: 40%;
  height: 355px;
  margin: auto;
  padding-bottom: 20px;
  margin-bottom: 20px;
  transition: all 0.5s ease-in-out;
  border-radius: 25px;
  font-size: 16px;
  min-width: 500px;
  font-weight: bold;
  text-align: center;
  border: 4px solid#4a6182;
}

.text-center {
  font-size: 30px;
  font-weight: bold;
  padding-top: 10px;
  padding-bottom: 25px;
}

.box-left {
  border-radius: 25px;
  background: #f7f7ff;
  width: 25%;
  height: 145px;
  margin-top: 35px;
  color: #4a6182;
  margin-left: 40px;
  
}
.text-left {
  font-size: 40px;
  font-weight: bold;
  padding-top: 36px;
}
.text-left img {
  vertical-align: middle;
}
.text-left a {
  font-size: 16px;
}

.center-box {
  background: #cce9ff;
  border-radius: 25px;
  margin-left: 20px;
  margin-right: 20px;
  padding: 10px;
}
.center {
  color: #f7f7ff;
  display: table-row;
  margin-left: 10px;
  margin-right: 10px;
}
.center h2 {
  margin-top: 4px;
  margin-bottom: 2px;
  padding-bottom: 0px;
}

.center h3 {
  font-size: 12px;
  margin-top: 0px;
  padding-bottom: 0px;
}

.small-green {
  width: 7%;
  height: 20px;
  display: table-cell;
  transition: all 0.5s ease-in-out;
  border-radius: 25px;
  background: #1e9d4c;
}
.small-yellow {
  width: 7%;
  height: 20px;
  display: table-cell;
  transition: all 0.5s ease-in-out;
  border-radius: 25px;
  background: #f3ba22;
}
.small-orange {
  width: 7%;
  height: 20px;
  display: table-cell;
  transition: all 0.5s ease-in-out;
  border-radius: 25px;
  background: #ea7e26;
}
.small-red {
  width: 7%;
  height: 20px;
  display: table-cell;
  transition: all 0.5s ease-in-out;
  border-radius: 25px;
  background: #e24c27;
}
.small-purple {
  width: 7%;
  height: 20px;
  display: table-cell;
  transition: all 0.5s ease-in-out;
  border-radius: 25px;
  background: #8962a1;
}

.green {
  color: #f7f7ff;
  text-align: center;
  float: right;
  height: 145px;;
  width: 50%;
  border-radius: 25px;
  margin-right: 40px;
  margin-top: -145px;
  background: #1e9d4c;
}
.yellow {
  color: #f7f7ff;
  text-align: center;
  float: right;
  height: 145px;;
  width: 50%;
  border-radius: 25px;
  margin-right: 40px;
  margin-top: -145px;
  background: #f3ba22;
}

.orange {
  color: #f7f7ff;
  text-align: center;
  float: right;
  height: 145px;;
  width: 50%;
  border-radius: 25px;
  margin-right: 40px;
  margin-top: -145px;
  background: #ea7e26;
}

.red {
  color: #f7f7ff;
  text-align: center;
  float: right;
  height: 145px;;
  width: 50%;
  border-radius: 25px;
  margin-right: 40px;
  margin-top: -145px;
  background: #e24c27;
}
.purple {
  color: #f7f7ff;
  text-align: center;
  float: right;
  height: 145px;
  width: 50%;
  border-radius: 25px;
  margin-right: 40px;
  margin-top: -145px;
  background: #8962a1;
}
#uv:hover {
  transition: all 0.5s ease-in-out;
}

@media only screen and (max-width: 1024px) {
  #uv {
    width: 90%;
  }
}
</style>