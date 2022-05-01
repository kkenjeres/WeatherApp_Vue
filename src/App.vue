<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <preloader />
    <main>
      <div class="search-box">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="Wheather in" 
        v-model="query"
        @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="temp">feels like{{ Math.round(weather.main.feels_like) }}°c</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import preloader from './preloader.vue'
export default {
  components: {
    preloader
  },
  name: 'app',
  data() {
    return{
      api_key: 'YOUR API KEY', 
      url_base: "https://api.openweathermap.org/data/2.5/",  
      query: "" ,
      weather: {}
    }
  },
  methods:{
    fetchWeather(e) {
      if(e.key =="Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
          this.query = "";
      }
    },
    
    setResults (results) {
      this.weather = results;
  },
  dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  }
}
</script>
const days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]; 
            let d = new Date();
           
            let day = days[d.getDay()];
            document.getElementById("demo").innerHTML = day;
          }       
<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'montserrat', sans-serif;
  font-size: 15px;
}

#app {
  background: url('./assets/img/cloud.jpg');
  background-size: cover;
  background-position: center;
  transition-delay: 0.7s;
}
#app.warm{
  transition: 0.9s;
  background: url('./assets/img/sunset.jpg');
  background-position: center;
}
main{
  min-height: 100vh;
  padding: 25px;
  
}
.search-box{
  text-align: center;
  margin: 40px 0 100px 0;
}
.search-bar{
  width: 60%;
  padding: 15px;
  font-size: 20px;
  font-style: italic;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
  color: #313131;
  border: none;
  outline: none;
  border-radius: 0 25px 0 25px;
  background-color: rgba(255, 255, 255, 0.7);
  transition: 0.4s;
}

.search-bar:focus{
  box-shadow: 0 0 16px rgba(0, 0, 0, 0.5);
  background-color: rgba(255, 255, 255, 0.85);
  border-radius: 25px 0px 25px 0px;
}
.location{
  margin-bottom: 10px;
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.date{
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.temp{
  width: 60%;
  text-align: center;
  margin: 30px auto;
  font-size: 102px;
  font-weight: 900;
  color: #fff;
  padding: 10px;
  background-color: rgba(0, 0, 0, 0.226);
  border-radius: 15px;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.weather{
  text-align: center;
  font-size: 50px;
  font-weight: 700;
  font-style: italic;
  color: #fff;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
