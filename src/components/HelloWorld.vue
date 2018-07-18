<template lang="pug">
.main
  .center-flex
    h1 Airport EC261
  .center-flex
    input(
      v-model="search",
      type="text",
      placeholder="Find airport"
      )
  .center-flex
    table
      thead
        tr
        th IATA
        th EC261
        th Name
        th Country
        th City
      tbody
        tr(
          v-for='airport in airports',
          :class = "airport['ec261'] ? 'bg-true' : 'bg-false' ",
          )
          th {{ airport['iata'] }}
          th {{ airport['ec261'] }}
          th {{ airport['name'] }}
          th {{ airport['country'] }}
          th {{ airport['city'] }}
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data () {
    return {
      search: '',
      airports: [],
      msg: 'Welcome to Your Vue.js App'
    }
  },
  watch: {
    search: function (val) {
      if (val.length > 0) {
        axios.get(`https://cors.io/?https://app.airhelp.com/api/airports?with_metropolitan_areas=false&q=${val}`)
          .then((response) => {
            this.airports = []
            response.data.airports.map(airport => {
              this.airports.push(airport)
            })
          })
      }
    }
  }
}
</script>

<style scoped lang="sass" src="../assets/sass/main.sass">
</style>
