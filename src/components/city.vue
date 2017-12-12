<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="cities.name" placeholder="Enter City name"/>
    <br /><br />
    <button @click="addCity">Add City</button>
    <br /><br /><br /><br />
    <h1>{{ msg2 }}</h1>
    <center>
    <table border="1">
        <thead>
            <tr>
                <th>City</th>
                <th>View</th>
                <th>Delete</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="city in cities">
                <td>{{city.name}}</td>
                <td><router-link :to="'/city/' + city.name">View</router-link></td>
                <td><a href="#" @click="deleteCity(city)">Remove</a></td>
            </tr>
        </tbody>
    </table>
    </center>
  </div>
</template>

<script>
export default {
  name: 'City',
  data () {
    return {
      msg: 'Welcome to Weather report App',
      msg2: 'Cities List'
    }
  },
  computed: {
      cities(){
          return this.$store.state.cities
      }
  },
  methods: {
      addCity(){
          this.$store.state.cities.push({
              name: this.$store.state.cities.name
          })
          this.cities.name = "";
      },
      deleteCity(city){
          this.$store.state.cities.splice(this.cities.indexOf(city), 1);
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
