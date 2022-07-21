<template>
    <div class="container">
        <div class="row mt-4">
            <div class="col-6">
                <ul v-for="element in films" :key="element.id">
                    <li>{{ element.original_title }}</li>
                    <li>{{ element.title }}</li>
                    <li>{{ element.original_language }}</li>
                    <li>{{ element.vote_average }}</li>
                    <li><span :class="`fi fi-${mapLang(element.original_language)}`"></span></li>
                </ul>
            </div>
            <div class="col-6">
                <ul v-for="element in tvs" :key="element.id">
                    <li>{{ element.original_name }}</li>
                    <li>{{ element.name }}</li>
                    <li>{{ element.original_language }}</li>
                    <li>{{ element.vote_average }}</li>
                    <li><span :class="`fi fi-${mapLang(element.original_language)}`"></span></li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        films: Array,
        tvs: Array
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