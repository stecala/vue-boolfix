<template>
    <div class="pt-4 container-fluid ps-4 mb-2 pb-5 ">
        <div class="row cont-card mx-auto">
            <h3>Film del momento:</h3>
            <hr class="ms-2">
            <div v-for="element in mostPopularMoviesList" :key="element.id" class="img-card-size position-relative">
                <img :src="completePosterPathW342(element.poster_path)" :alt="element.title">
                <div>
                <a :href="linkToYT(element)">click
                </a>
        </div>
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
        linkToYT(element){
            let link = element.original_title.replaceAll(' ','+')
            return  'https://www.youtube.com/results?search_query='+link
        }  
    },
    data :  function(){
        return{
        
        }
    }
}
</script>

<style>

</style>