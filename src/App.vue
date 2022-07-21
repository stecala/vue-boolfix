<template>
  <div id="app">
    <HeaderApp @filmSearched='setTxtSearched' />
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
      txtSearch : '',
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

        this.filmsOriginalTitle=[]
        this.filmsTitle=[]
        this.filmsLanguage=[]
        this.filmsRate=[]

        for(let i=0; i< result.data.results.length; i++){
          this.filmsOriginalTitle.push( result.data.results[i].original_title)
          this.filmsTitle.push( result.data.results[i].title)
          this.filmsLanguage.push( result.data.results[i].original_language)
          this.filmsRate.push( result.data.results[i].vote_average) 
        }
        
        console.log({'titolo originale' : this.filmsOriginalTitle, 'titolo' : this.filmsTitle, 'lingua' : this.filmsLanguage, 'voto' : this.filmsRate})
      })
      .catch((error) => {
        console.warn(error)
      })
    },
    setTxtSearched(choice){
      this.txtSearch = `&query=${choice}`
      this.APICall()
    },
  },
  created (){
    this.setTxtSearched(this.txtSearch)
  }
}
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";

</style>
