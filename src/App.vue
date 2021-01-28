<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 27 ? 'warm' : ''">
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
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      api_key: '356eedcb664298728c52f42044631bd4',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },

  methods: {
    fetchWeather (e) {
      if (e.key == 'Enter') {
        fetch(`${this.url_base}weather?q=${this.query.trim()}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },

    setResults (results) {
      this.weather = results;
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

  #app {
    background-color: rgb(144, 207, 209);
    background-image: url('./assets/cold.jpg');
    transition: 0.4s;
  }

  main {
    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.20), rgba(0, 0, 0, 0.60));
    background-size: cover;
  }

  #app.warm {
    background-image: url('./assets/warm.jpg');
    background-size: cover;
  }
</style>
