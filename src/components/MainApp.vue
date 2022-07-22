<template>
    <main class="container-fluid">
        <div class="row">
            <div class="col-6">
                <div >
                    <FilmsCard :films="films" />
                    <!-- <li><img :src="completePosterPathW342(element.poster_path)" :alt="element.title"></li>
                    <li>{{ element.original_title }}</li>
                    <li>{{ element.title }}</li>
                    <li>{{ element.original_language }}</li>
                    <li>{{ changeValueVote(element.vote_average) }}</li>
                    <li><span :class="`fi fi-${mapLang(element.original_language)}`"></span></li> -->
                </div>
            </div>
            <div class="col-6">
                <ul v-for="element in tvs" :key="element.id">
                    <li><img :src="completePosterPathW342(element.poster_path)" :alt="element.title"></li>
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
import FilmsCard from './FilmsCard.vue'
export default {
    components : {
        FilmsCard,
    },
    props: {
        films: Array,
        tvs: Array,
    },
    data: function () {
        return {};
    },
    methods: {
        mapLang(lang) {
            console.log(this.films);
            switch (lang) {
                case "en":
                    return "gb";
                case "ja":
                    return "jp";
                case "ko":
                    return "kr";
                case "el":
                    return "gr";
                case "er":
                    return "il";
                case "fa":
                    return "ir";
                case "zh":
                    return "cn";
                case "cs":
                    return "cz";
                case "nb":
                    return "no";
                case "hi":
                    return "in";
                default:
                    return lang;
            }
        },
        
        changeValueVote(vote) {
            let voteIn5 = Math.ceil((vote * 5) / 10);
            let stars = "";
            switch (voteIn5) {
                case 0:
                    stars = "0";
                    break;
                case 1:
                    stars = "⭐";
                    break;
                case 2:
                    stars = "⭐⭐";
                    break;
                case 3:
                    stars = "⭐⭐⭐";
                    break;
                case 4:
                    stars = "⭐⭐⭐⭐";
                    break;
                case 5:
                    stars = "⭐⭐⭐⭐⭐";
                    break;
                default:
                    console.warn("voteIn5 non e' riconosciuto ", { voteIn5 });
            }
            return stars;
        }
    },
}
</script>
<style scoped lang="scss">
@import '../assets/style/variable.scss';

main{

    min-height: calc(100vh - 100px);
    background-color: $bgColorMain;
     ul{
        list-style-type: none;
        border: 1px solid black;
    }
}
</style>