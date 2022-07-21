<template>
    <div class="container">
        <div class="row">
            <div class="col-6">
                <ul v-for="( element, index ) in films" :key="index">
                    <li>{{ films[index].original_title }}</li>
                    <li>{{ films[index].title }}</li>
                    <li>{{ films[index].original_language }}</li>
                    <li>{{ films[index].vote_average }}</li>
                    <li><span :class="`fi fi-${mapLang(films[index].original_language)}`"></span></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        films: Array
    },
    methods:{
        mapLang(lang){
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
    }
}
</script>

<style scoped lang="scss">
</style>