<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <center>
      <select v-model="city" @change="changeCity(city.name)"><option v-for="city in cities" v-bind:value="city">{{city.name}}</option></select>
      <br/>
    <table border="1">
      <thead>
          <tr>
            <th>Time</th>
            <th>Humidity</th>
            <th>Weather</th>
            <th>Wind Speed</th>
          </tr>
      </thead>
      <tbody>
        <tr v-for="(report, index) in reports.list" v-if="index < 8">
          <td>{{report.dt_txt.split(" ")[1]}}</td>
          <td>{{report.main.humidity}}</td>
          <td v-for="weat in report.weather">{{weat.description}}</td>
          <td>{{report.wind.speed}}</td>
        </tr>
      </tbody>
    </table>
    </center>
  </div>
</template>

<script>
export default {
  name: 'Report',
  data () {
    return {
      msg: 'Weather Report',
      reports: [],
      city: {
        name: this.$route.params.city
      }
    }
  },
  created(){
      // this.$http.get('http://api.openweathermap.org/data/2.5/forecast?q='+this.$route.params.city+'&appid=c2ede116d31fab7ebcd0ec777d0f2310')
      // .then(function(response){
      //   this.reports = response.data
      this.changeCity(this.$route.params.city)
  },
  computed: {
    cities(){
      return this.$store.state.cities
    }
  },
  methods: {
    changeCity(city){
      this.$http.get('http://api.openweathermap.org/data/2.5/forecast?q='+city+'&appid=c2ede116d31fab7ebcd0ec777d0f2310')
      .then(function(response){
        this.reports = response.data
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
  color: #42b983;
}
</style>
