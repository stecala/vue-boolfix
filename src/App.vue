<template>
  <div id="app">
    <HeaderApp />
  </div>
</template>

<script>
import HeaderApp from './components/HeaderApp.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    HeaderApp,
  },
  data: function(){
    return{
      apiKey : '?api_key=290ef3b32debba72662776b92b209938',
      apiLink : 'https://api.themoviedb.org/3/search/',
      movie : 'movie',
      txtSearch : '&query=fantozzi',
      films : [],
      }
  },
  methods: {
    APICall() {
      axios.get(`${this.apiLink}${this.movie}${this.apiKey}${this.txtSearch}`)
      .then((result) => {
        this.films = result.data.results[1].original_title
        console.log(this.films)
      })
      .catch((error) => {
        console.warn(error)
      })
    },
  },
  created (){
    this.APICall()
  }
}
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";

</style>
