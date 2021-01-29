<template>
  <div id="app" class="h-screen">
    <main class="h-full">
      <div class="h-2/3 p-20 object-center bg-cover backgroundImage">
        <div class="grid grid-cols-2 h-1/3">
          <div class="flex flex-col place-content-between">
            <div>
              <span class="text-white text-9xl font-semibold custom-shadow">{{ ampmTime[0] }}</span>
              <span class="text-white text-2xl ml-3 custom-shadow">{{ ampmTime[1] }}</span>
            </div>
            <div class="date text-white text-2xl custom-shadow ml-2">{{ dateBuilder() }}</div>
          </div>
          <div v-if="typeof weather.main != 'undefined'" class="flex flex-col mt-7 items-end">
            <div class="relative text-gray-600">
              <input class="border-2 border-gray-300 bg-white h-10 px-5 pr-16 rounded-lg text-sm focus:outline-none"
                type="text" name="search" placeholder="Search" v-model="query" @keypress="fetchWeather">
                <button @click="fetchWeatherClick()" class="absolute right-0 top-0 mt-3 mr-3 focus:outline-none">
                  <svg class="text-gray-600 h-4 w-4 fill-current" xmlns="http://www.w3.org/2000/svg"
                    xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px"
                    viewBox="0 0 56.966 56.966" style="enable-background:new 0 0 56.966 56.966;" xml:space="preserve"
                    width="512px" height="512px">
                    <path
                      d="M55.146,51.887L41.588,37.786c3.486-4.144,5.396-9.358,5.396-14.786c0-12.682-10.318-23-23-23s-23,10.318-23,23  s10.318,23,23,23c4.761,0,9.298-1.436,13.177-4.162l13.661,14.208c0.571,0.593,1.339,0.92,2.162,0.92  c0.779,0,1.518-0.297,2.079-0.837C56.255,54.982,56.293,53.08,55.146,51.887z M23.984,6c9.374,0,17,7.626,17,17s-7.626,17-17,17  s-17-7.626-17-17S14.61,6,23.984,6z" />
                  </svg>
                </button>
            </div>
            <span class="text-white text-5xl font-bold custom-shadow mt-3">{{ weather.name }}</span>
            <span class="text-white text-2xl font-bold custom-shadow mt-1">{{ weather.sys.country }}</span>
          </div>
        </div>
      </div>
      <div v-if="typeof weather.main != 'undefined'" class="grid grid-cols-7 h-1/3 bg-gray-800">
        <div class="grid grid-cols-3 col-span-2 px-14 place-items-center">
          <img :src="currentIconUrl" alt="Weather Icon" class="col-span-2 w-72 h-72">
          <div class="flex flex-col justify-around">
            <span class="text-white text-xl font-semibold text-center py-2 rounded-full bg-gray-900">CURRENTLY</span>
            <span class="text-white text-8xl text-center font-semibold">{{ Math.round(weather.main.temp) }}°c</span>
          </div>
        </div>
        <div class="grid grid-rows-5 py-9 place-items-center">
          <span class="text-white text-lg font-semibold text-center rounded-full bg-gray-900 self-center w-2/5 py-1">{{ ampmForecast[0][0] }} {{ ampmForecast[0][1] }}</span>
          <img :src="forecastIconUrl[0]" alt="Weather Icon" class="row-span-3 w-32 h-32">
          <span class="text-white text-5xl text-center font-semibold">{{ Math.round(forecast.list[0].main.temp) }}°c</span>
        </div>
        <div class="grid grid-rows-5 py-9 place-items-center">
          <span class="text-white text-lg font-semibold text-center rounded-full bg-gray-900 self-center w-2/5 py-1">{{ ampmForecast[1][0] }} {{ ampmForecast[1][1] }}</span>
          <img :src="forecastIconUrl[1]" alt="Weather Icon" class="row-span-3 w-32 h-32">
          <span class="text-white text-5xl text-center font-semibold">{{ Math.round(forecast.list[1].main.temp) }}°c</span>
        </div>
        <div class="grid grid-rows-5 py-9 place-items-center">
          <span class="text-white text-lg font-semibold text-center rounded-full bg-gray-900 self-center w-2/5 py-1">{{ ampmForecast[2][0] }} {{ ampmForecast[2][1] }}</span>
          <img :src="forecastIconUrl[2]" alt="Weather Icon" class="row-span-3 w-32 h-32">
          <span class="text-white text-5xl text-center font-semibold">{{ Math.round(forecast.list[2].main.temp) }}°c</span>
        </div>
        <div class="grid grid-rows-5 py-9 place-items-center">
          <span class="text-white text-lg font-semibold text-center rounded-full bg-gray-900 self-center w-2/5 py-1">{{ ampmForecast[3][0] }} {{ ampmForecast[3][1] }}</span>
          <img :src="forecastIconUrl[3]" alt="Weather Icon" class="row-span-3 w-32 h-32">
          <span class="text-white text-5xl text-center font-semibold">{{ Math.round(forecast.list[3].main.temp) }}°c</span>
        </div>
        <div class="grid grid-rows-5 py-9 place-items-center">
          <span class="text-white text-lg font-semibold text-center rounded-full bg-gray-900 self-center w-2/5 py-1">{{ ampmForecast[4][0] }} {{ ampmForecast[4][1] }}</span>
          <img :src="forecastIconUrl[4]" alt="Weather Icon" class="row-span-3 w-32 h-32">
          <span class="text-white text-5xl text-center font-semibold">{{ Math.round(forecast.list[4].main.temp) }}°c</span>
        </div>
      </div>
    </main>
  </div>

  <!-- <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 27 ? 'warm' : ''">
    <main class="p-5 h-screen">
      <div class="search-box w-full mb-3">
        <input type="text" class="search-bar block w-full p-3 appearance-none border-none bg-none bg-white opacity-50 outline-none focus:outline-none focus:opacity-70 focus:rounded-tl-xl focus:rounded-br-xl focus:rounded-bl-none focus:rounded-tr-none focus:shadow-lg rounded-bl-xl rounded-tr-xl transition-all duration-500" placeholder="Search..." v-model="query" @keypress="fetchWeather">
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="locaton-box">
          <div class="location text-white text-2xl font-bold text-center text-shadow-md">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date text-white text-xl font-light text-center text-shadow-md">{{ dateBuilder() }}</div>
        </div>
        <div class="weather-box text-center">
          <div class="temp inline-block px-5 py-6 m-4 text-white text-7xl font-extrabold text-shadow-md bg-gray-50 bg-opacity-25 rounded-lg shadow-md">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="weather text-white text-2xl font-bold text-shadow-md capitalize">{{ weather.weather[0].description }}</div>
        </div>
      </div>
    </main>
  </div> -->
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      api_key: '356eedcb664298728c52f42044631bd4',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: 'London, GB',
      weather: {},
      forecast: {},
      ampmTime: this.currentTime(),
      ampmForecast: [],
      currentIconUrl: String,
      forecastIconUrl: []
    }
  },

  created() {
    window.setInterval(() => {
        this.ampmTime = this.currentTime()
        this.ampmForecast[0] = this.forecastTime(3)
        this.ampmForecast[1] = this.forecastTime(6)
        this.ampmForecast[2] = this.forecastTime(9)
        this.ampmForecast[3] = this.forecastTime(12)
        this.ampmForecast[4] = this.forecastTime(15)
    },5 * 1000);
  },

  mounted() {
      fetch(`${this.url_base}weather?q=${this.query.trim()}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        })
        .then(this.weatherResults)
        .then(this.getCurrentIcon);

      fetch(`${this.url_base}forecast?q=${this.query.trim()}&units=metric&cnt=5&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        })
        .then(this.forecastResults)
        .then(this.getForecastIcon);
  },

  methods: {
    fetchWeather (e) {
      if (e.key == 'Enter') {
        fetch(`${this.url_base}weather?q=${this.query.trim()}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          })
          .then(this.weatherResults)
          .then(this.getCurrentIcon);
      }
    },

    fetchWeatherClick() {
      fetch(`${this.url_base}weather?q=${this.query.trim()}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        })
        .then(this.weatherResults)
        .then(this.getCurrentIcon);
    },

    weatherResults (results) {
      this.weather = results;
    },

    forecastResults (results) {
      this.forecast = results;
    },

    dateBuilder () {
      let d = new Date();
      let months = [
        'January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July',
        'August',
        'September',
        'October',
        'November',
        'December'
      ];
      let days = [
        'Sunday',
        'Monday',
        'Tuesday',
        'Wednesday',
        'Thursday',
        'Friday',
        'Saturday'
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    },

    currentTime() {
      let d = new Date();
      let hours = d.getHours();
      let minutes = d.getMinutes();
      let ampm = hours >= 12 ? 'PM' : 'AM';
      hours = hours % 12;
      hours = hours ? hours : 12;
      minutes = minutes < 10 ? '0' + minutes : minutes;
      let hrsMins = hours + ':' + minutes;
      return [hrsMins, ampm];
    },

    forecastTime(hrs) {
      let d = new Date();
      let hours = d.getHours() + hrs;
      let minutes = d.getMinutes();
      let ampm = hours >= 12 ? 'PM' : 'AM';
      hours = hours % 12;
      hours = hours ? hours : 12;
      minutes = minutes < 10 ? '0' + minutes : minutes;
      let hrsMins = hours + ':' + minutes;
      return [hrsMins, ampm];
    },

    getCurrentIcon() {
      this.currentIconUrl = 'https://openweathermap.org/img/wn/' + this.weather.weather[0].icon + '@4x.png';
    },

    getForecastIcon() {
      this.forecastIconUrl[0] = 'https://openweathermap.org/img/wn/' + this.forecast.list[0].weather[0].icon + '@4x.png';
      this.forecastIconUrl[1] = 'https://openweathermap.org/img/wn/' + this.forecast.list[1].weather[0].icon + '@4x.png';
      this.forecastIconUrl[2] = 'https://openweathermap.org/img/wn/' + this.forecast.list[2].weather[0].icon + '@4x.png';
      this.forecastIconUrl[3] = 'https://openweathermap.org/img/wn/' + this.forecast.list[3].weather[0].icon + '@4x.png';
      this.forecastIconUrl[4] = 'https://openweathermap.org/img/wn/' + this.forecast.list[4].weather[0].icon + '@4x.png';
    }
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'montserrat', sans-serif;
  }

  /* #app {

  } */

  .backgroundImage {
    background-image: url('./assets/cold.jpg');
    background-size: cover;
    transition: 0.4s;
  }

  main {
    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.20), rgba(0, 0, 0, 0.60));
    background-size: cover;
  }

  .custom-shadow {
    text-shadow: 3px 2px 2px rgba(0, 0, 0, 0.6);
  }

  #app.warm {
    background-image: url('./assets/warm.jpg');
    background-size: cover;
  }
</style>
