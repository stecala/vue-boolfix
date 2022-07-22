<template>
  <div v-for="element in films" :key="element.it">
        <img :src="completePosterPathW342(element.poster_path)" :alt="element.title">
  </div>
</template>

<script>
export default {
  components: {
    
  },
  data: function(){
    return{
     
      }
  },
  methods: {
    completePosterPathW342(path) {
            if (path != null || path == "") {
                path = `https://image.tmdb.org/t/p/w342/${path}`;
            }
            else {
                path = "/defaultw-342.jpg";
            }
            return path;
        },
  },
  props: {
        films: Array,
    },
  created (){
    console.alert(this.films)
  }
}
</script>

<style lang="scss">

</style>