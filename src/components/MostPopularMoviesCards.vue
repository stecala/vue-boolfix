<template>
    <div class="pt-4 container-fluid ps-4 mb-2 pb-5 ">
        <div class="row cont-card mx-auto">
            <h3>Lista dei Film più Popolari:</h3>
            <hr class="ms-2">
            <div v-for="element in mostPopularMoviesList" :key="element.id" class="img-card-size position-relative">
                <img :src="completePosterPathW342(element.poster_path)" :alt="element.title">
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props :{
        mostPopularMoviesList : Array,
    },
    methods:{
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
    data :  function(){
        return{
        
        }
    }
}
</script>

<style>

</style>