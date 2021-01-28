<template>
  <div>
    <main class="p-5 h-screen">
      <div class="search-box w-full mb-3">
        <input type="text" class="search-bar block w-full p-3 appearance-none border-none bg-none bg-white opacity-50 outline-none focus:outline-none focus:opacity-70 focus:rounded-tl-xl focus:rounded-br-xl focus:rounded-bl-none focus:rounded-tr-none focus:shadow-lg rounded-bl-xl rounded-tr-xl transition-all duration-300" placeholder="Search...">
      </div>

      <div class="weather-wrap">
        <div class="locaton-box">
          <div class="location text-white text-2xl font-bold text-center text-shadow-md">Cyberjaya, Malaysia</div>
          <div class="date text-white text-xl font-light text-center text-shadow-md">Monday 20 January 2020</div>
        </div>
        <div class="weather-box text-center">
          <div class="temp inline-block px-5 py-6 m-4 text-white text-7xl font-extrabold text-shadow-md bg-gray-50 bg-opacity-25 rounded-lg shadow-md">9°c</div>
          <div class="weather text-white text-2xl font-bold text-shadow-md">Rain</div>
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
      api_key: '356eedcb664298728c52f42044631bd4'
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

  #app {
    background-color: rgb(144, 207, 209);
    transition: 0.4s;
  }
</style>
