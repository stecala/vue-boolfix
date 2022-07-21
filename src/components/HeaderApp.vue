<template>
  <header>
    <div class="container-fluid ">
      <div class="row">
        <div class="col-4 d-flex align-items-center mt-1">
          <a href="#"><img src="/logo.png" alt="logo netflix"></a>
        </div>
        <div class="col-8 d-flex align-items-center justify-content-end">
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
@import '../assets/style/variable.scss';
header{
  background-color: $bgColorMain;
  height: 100px;
  img{
    width: 150px;
  }
}
</style>
