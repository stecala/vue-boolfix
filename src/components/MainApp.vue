<template>
    <main class="container">
        <div class="row mt-4">
            <div class="col-6">
                <ul v-for="element in films" :key="element.id">
                    <li><img :src="completePosterPath(element.poster_path)" :alt="element.title"></li>
                    <li>{{ element.original_title }}</li>
                    <li>{{ element.title }}</li>
                    <li>{{ element.original_language }}</li>
                    <li>{{ element.vote_average }}</li>
                    <li><span :class="`fi fi-${mapLang(element.original_language)}`"></span></li>
                </ul>
            </div>
            <div class="col-6">
                <ul v-for="element in tvs" :key="element.id">
                    <li><img :src="completePosterPath(element.poster_path)" :alt="element.title"></li>
                    <li>{{ element.original_name }}</li>
                    <li>{{ element.name }}</li>
                    <li>{{ element.original_language }}</li>
                    <li>{{ element.vote_average }}</li>
                    <li><span :class="`fi fi-${mapLang(element.original_language)}`"></span></li>
                </ul>
            </div>
        </div>
    </main>
</template>

<script>
export default {
    props: {
        films: Array,
        tvs: Array,
    },
    methods:{
        mapLang(lang){
            console.log(this.films)

            switch(lang){
                case 'en' :
                    return 'gb'
                case 'ja' :
                    return 'jp'
                case 'ko' :
                    return 'kr'
                default :
                    return lang
            }
        },
        completePosterPath(path){
            if(path != null){
                path = `https://image.tmdb.org/t/p/w500/${path}`
            }
            else{
                path ='/defaultw-500.jpg'
            }
            return  path
        }, 
    }
}
</script>

<style scoped lang="scss">
</style>