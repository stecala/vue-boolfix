<template>
    <main class="container">
        <div class="row mt-4">
            <div class="col-6">
                <ul v-for="element in films" :key="element.id">
                    <li><img :src="completePosterPath(element.poster_path)" :alt="element.title"></li>
                    <li>{{ element.original_title }}</li>
                    <li>{{ element.title }}</li>
                    <li>{{ element.original_language }}</li>
                    <li>{{ changeValueVote(element.vote_average) }}</li>
                    <li><span :class="`fi fi-${mapLang(element.original_language)}`"></span></li>
                </ul>
            </div>
            <div class="col-6">
                <ul v-for="element in tvs" :key="element.id">
                    <li><img :src="completePosterPath(element.poster_path)" :alt="element.title"></li>
                    <li>{{ element.original_name }}</li>
                    <li>{{ element.name }}</li>
                    <li>{{ element.original_language }}</li>
                    <li>{{ changeValueVote(element.vote_average) }}</li>
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
    data : function(){
        return{

        }    
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
            if(path != null || path == ''){
                path = `https://image.tmdb.org/t/p/w500/${path}`
            }
            else{
                path ='/defaultw-500.jpg'
            }
            return  path
        },
        changeValueVote(vote){
            console.log(vote)
            let voteIn5 = Math.ceil((vote*5)/10)
            console.log(voteIn5)
            let stars = ''
            switch(voteIn5){
                case 0 :
                    stars = '0'
                    break
                case 1 :
                    stars = '⭐'
                     break
                case 2 :
                    stars = '⭐⭐'
                    break
                case 3 :
                    stars = '⭐⭐⭐'
                    break
                case 4 :
                    stars = '⭐⭐⭐⭐'
                    break
                case 5 :
                    stars = '⭐⭐⭐⭐⭐'
                    break
                default :
                    console.warn('voteIn5 non e\' riconosciuto ',{voteIn5})
            } 
            return stars

        } 

    }
}
</script>

<style scoped lang="scss">
</style>