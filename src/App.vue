<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
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
  data : function(){
    return {
      api_key : '290ef3b32debba72662776b92b209938',
    },
  }
}
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";

</style>
