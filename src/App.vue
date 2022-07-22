<template>
  <div id="app">
    <HeaderApp @filmSearched='setTxtSearched' />
    <MainApp :films="films" :tvs="tvs" :movieGenreList="movieGenreList" />
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
      apiLinkGenreMovie : 'https://api.themoviedb.org/3/genre/movie/list',
      tv : 'tv',
      movie : 'movie',
      txtSearch : '',
      films : [],
      tvs : [],
      movieGenreList :[]
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
    APICallGenre(){
      axios.get(this.apiLinkGenreMovie+this.apiKey)
      .then((result)=>{
        this.movieGenreList = result.data.genres
      })
      .catch((error)=>{
        console.warn(error``)
      })
    },
    setTxtSearched(choice){
      this.txtSearch = `&query=${choice}`
      this.APICallMovie()
      this.APICallTvs()
      this.APICallGenre()
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
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300;0,400;0,500;0,700;0,800;1,300;1,400;1,500;1,600;1,700;1,800&display=swap');
body{
  color: white;
  font-family: 'Open Sans', sans-serif;

}
</style>
