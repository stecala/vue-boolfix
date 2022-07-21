<template>
  <header class="bg-dark text-white">
    <div class="container">
      <div class="row align-items-center p-4">
        <div class="col-4">
          <h1>Header</h1>
        </div>
        <div class="col-8 text-end">
          <input type="text" placeholder="Cerca un Film" v-model="filmSearched">
          <a class="btn btn-primary ms-2 " @click="sendFilmSearched()">Cerca</a>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  props: {
  },
  data: function () {
    return {
      filmSearched: '',
    }
  },
  methods: {
    sendFilmSearched() {
      this.$emit('filmSearched', this.filmSearched)
      this.filmSearched = ''
    }
  },
}
</script>

<style scoped lang="scss">
</style>
