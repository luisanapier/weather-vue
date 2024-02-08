<!-- <script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script> -->

<template>
  <div id="app">
      <main>
        <div class="search-box">
          <input
          type="text"
          class="search-bar"
          placeholder="Search..." 
          v-model="query"
          v-on:keypress="getWeather"
          />
        </div>

  <div class="weather-wrap">
    <div class="location-box">
      <div class="location"> {{  }}</div>
      <div class="date"> {{  }}</div>
    </div>

    <div class="weather-box">
      <div class="temp"> 5c </div>
      <div class="weather"> Cloudy </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      api_key: "6c384f1694fcb2d884c5c5948e248191",
      url_base: "https://api.openweathermap.org/data/3.0/onecall?",
      query: '',
      weather: {}
    }
  },
  methods: {
    getWeather(evt) {
    
      if (evt.key == "Enter") {
        fetch(`http://api.openweathermap.org/geo/1.0/direct?q=${this.query}&appid=${this.api_key}`)
        .then((response) => response.json())
        .then((result) => {
          fetch(`${this.url_base}lat=${result[0].lat}&lon=${result[0].lon}&units=metric&appid=${this.api_key}`)
          .then((rspns) => rspns.json())
          .then((this.setResults,
          console.log(weather) 
          ));
          })
        }
      },
      setResults(results) {
        this.weather = results;
      },
      dateBuilder () {
        let d = new Date(); 
        let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]
        let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"]

        let day = days[d.getDay()];
        let date = d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();

        return `${day}, ${date} ${month} ${year}`;
      }
    }
  };
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: center;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.location-box .location {
  color: #fff;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  font-size: 32px;
  font-weight: 500;
}

.location-box .date {
  color: #fff;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.15);
  font-size: 20px;
  font-weight: 400;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 100px;
  font-weight: 900;

  margin: 30px 0px;
}

.weather-box .weather {
  display: block;
  color: #fff;
  font-size: 48px;
  font-weight: 100;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  font-style: italic;
}
</style>
