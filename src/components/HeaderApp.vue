<template>
  <div >
        <input type="text" placeholder="Cerca un Film" class="mt-2 ms-2" v-model="filmSearched">
        <a class="btn btn-primary ms-2 mt-2" @click="sendFilmSearched()">Cerca</a>
  </div>
</template>

<script>
export default {
  props: {
  },
  data : function(){
    return{
      filmSearched : '',
      }
  },
  methods: {
    sendFilmSearched(){
      this.$emit('filmSearched', this.filmSearched)
      this.filmSearched = ''
    }
  },  
}
</script>

<style scoped lang="scss">

</style>
