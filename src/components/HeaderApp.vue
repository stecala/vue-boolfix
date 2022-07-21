<template>
  <header>
    <div class="container-fluid ">
      <div class="row">
        <div class="col-4 d-flex align-items-center mt-1 ps-4">
          <a href="#"><img src="/logo.png" alt="logo netflix"></a>
        </div>
        <div class="col-8 d-flex align-items-center justify-content-end  pe-4">
          <span @click="changeStatutsClicked()" v-if="(isClicked == false)">🔍</span>
          <input type="text" placeholder="Cerca un Film, Serie TV" v-model="filmSearched" class="my-input-txt p-2" @keyup.enter="sendFilmSearched()" v-if="isClicked" v-on:blur="changeStatutsClicked()" ref="input">
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
      isClicked : false,
    }
  },
  methods: {
  
    sendFilmSearched() {
      this.$emit('filmSearched', this.filmSearched)
      this.filmSearched = ''
    },
    changeStatutsClicked(){
      this.filmSearched = '',
      this.isClicked = !this.isClicked
    },

  },
}
</script>

<style scoped lang="scss">
@import '../assets/style/variable.scss';
header{
  background-color: $bgColorMain;
  height: 100px;
  span{
    cursor: pointer;
  }
  .my-input-txt{
    background-color: $bgColorMain;
    color: white;
    border: solid 1px white;
  }
  img{
    width: 150px;
  }
}
</style>
