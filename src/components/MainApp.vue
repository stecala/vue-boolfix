<template>
  <div>
    <ul v-for="( element, index ) in films" :key="index">
       <li>{{films[index].original_title}}</li>
       <li>{{films[index].title}}</li>
       <li>{{films[index].original_language}}</li>
       <li>{{films[index].vote_average}}</li>
    </ul>
  </div>
</template>

<script>
export default {
 props: {
    films: Array
  },
}
</script>

<style scoped lang="scss">

</style>