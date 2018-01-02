<template>
  <div class="weather">
    <h4>Weather for {{ location }} </h4>
    <p> {{ temperature }}, {{ condition }}</p>
  </div>
</template>

<script>
const WEATHER_URL = 'https://query.yahooapis.com/v1/public/yql?q=select%20*%20from%20weather.forecast%20where%20woeid%20in%20(select%20woeid%20from%20geo.places(1)%20where%20text%3D%22nome%2C%20ak%22)&format=json&env=store%3A%2F%2Fdatatables.org%2Falltableswithkeys'

export default {
  name: 'hello',
  data () {
    return {
      location: '',
      temperature: '',
      text: '',
      condition: ''
    }
  },
  created () {
    this.fetchWeather()
  },
  methods: {
    async fetchWeather () {
      const response = await fetch(WEATHER_URL)
      const json = await response.json()
      const item = json.query.results.channel.item
      this.location = item.title
      this.temperature = item.condition.temp
      this.condition = item.condition.text
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #35495E;
}
</style>
