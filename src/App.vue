<template>
  <div id="app">
    <HeaderApp @filmSearched='setTxtSearched' />
    <MainApp :films="films" :tvs="tvs" />
  </div>
</template>

<script>
import HeaderApp from './components/HeaderApp.vue'
import MainApp from './components/MainApp.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    HeaderApp,
    MainApp,
  },
  data: function(){
    return{
      apiKey : '?api_key=290ef3b32debba72662776b92b209938',
      apiLink : 'https://api.themoviedb.org/3/search/',
      tv : 'tv',
      movie : 'movie',
      txtSearch : '',
      films : [],
      tvs : [],
      }
  },
  methods: {
    APICallMovie() {
      axios.get(`${this.apiLink}${this.movie}${this.apiKey}${this.txtSearch}`)
      .then((result) => {
        this.films = result.data.results
      })
      .catch((error) => {
        console.warn(error)
      })
    },
    APICallTvs(){
      axios.get(`${this.apiLink}${this.tv}${this.apiKey}${this.txtSearch}`)
      .then((result) => {
        this.tvs = result.data.results
      })
      .catch((error) => {
        console.warn(error)
      })
    },
    setTxtSearched(choice){
      this.txtSearch = `&query=${choice}`
      this.APICallMovie()
      this.APICallTvs()
    },
  },
  created (){
    this.setTxtSearched(this.txtSearch)
  }
}
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import "~flag-icons/css/flag-icons.css";

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

</style>
