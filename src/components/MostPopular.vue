<template>
    <div>
        <MostPopularMoviesCard :mostPopularMoviesList="mostPopularMoviesList" />
    
    </div>
</template>

<script>
import MostPopularMoviesCard from './MostPopularMoviesCard.vue'
export default {
    components :{
        MostPopularMoviesCard,
    },
    props: {
        mostPopularMoviesList : Array,
    }
}
</script>

<style>

</style>