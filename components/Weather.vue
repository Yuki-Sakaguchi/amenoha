<template>
  <div class="weather">
    <p class="error__text" v-if="errorText">{{ errorText }}</p>
    <input class="weather__input" type="text" v-model="target" @keyup.enter="getWeather" :class="{ error: isError }">
    <button class="weather__btn" @click="getWeather">取得</button>
    <div class="weather__info">
      <h3 class="weather__city">{{ this.city }}</h3>
      <div class="weather__data">
        気温 {{ this.temp }}°<br>
        最低気温 {{ this.minTemp }}°<br>
        最高気温 {{ this.maxTemp }}°<br>
        湿度 {{ this.humidity }}<br>
        気圧 {{ this.pressure }}<br>
        風向き {{ this.deg }}<br>
        風速 {{ this.speed }}
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      target: 'tokyo',
      city: null,
      temp: null,
      minTemp: null,
      maxTemp: null,
      humidity: null,
      pressure: null,
      deg: null,
      speed: null,
      errorText: null,
      isError: false,
    }
  },
  methods: {
    getWeather () {
      const API_KEY = 'd0aef5f25899f79a23c93e7b66b6c913'
      axios.get('https://api.openweathermap.org/data/2.5/weather', {
        params: {
          appid: API_KEY,
          units: 'metric',
          q: this.target+',jp',
        }
      }).then(responce => {
        console.log(responce)
        this.errorText = null
        this.isError = false

        this.city = responce.data.name
        this.temp = responce.data.main.temp
        this.minTemp = responce.data.main.temp_min
        this.maxTemp = responce.data.main.temp_max
        this.humidity = responce.data.main.humidity
        this.pressure = responce.data.main.pressure
        this.deg = responce.data.wind.deg
        this.speed = responce.data.wind.speed

        const img = 'http://openweathermap.org/img/w/'+responce.data.weather[0].icon+'.png'
        console.log(img);
      }).catch(error => {
        console.log(error)
        this.errorText = error
        this.isError = true
      })
    }
  },
  mounted () {
    this.getWeather()
  }
}
</script>

<style lang="scss">
.weather {
  margin-top: 50px;
  &__input {
    display: block;
    width: 60%;
    margin: auto;
    padding: 5px;
    font-size: 16px;
  }
  &__btn {
    background: gray;
    border: none;
    width: 120px;
    padding: 8px;
    color: white;
    border-radius: 5px;
    font-size: 16px;
    margin-top: 16px;
  }
  &__info {
    padding: 10px;
    border: 1px solid #ccc;
    margin-top: 30px;
  }
}

.error {
  border: 1px solid red;
  &__text {
    color: red;
  }
}
</style>
