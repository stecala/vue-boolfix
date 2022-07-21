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
      filmsOriginalTitle : [],
      filmsTitle : [],
      filmsLanguage : [],
      filmsRate : [],
      }
  },
  methods: {
    APICall() {
      axios.get(`${this.apiLink}${this.movie}${this.apiKey}${this.txtSearch}`)
      .then((result) => {
        this.filmsOriginalTitle = result.data.results[1].original_title
        this.filmsTitle = result.data.results[1].title
        this.filmsLanguage = result.data.results[1].original_language
        this.filmsRate = result.data.results[1].vote_average
        console.log({'titolo originale' : this.filmsOriginalTitle, 'titolo' : this.filmsTitle, 'lingua' : this.filmsLanguage, 'voto' : this.filmsRate})
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
