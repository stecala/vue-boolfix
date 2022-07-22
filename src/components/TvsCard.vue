<template>
  <div class="pt-4 container-fluid ps-4 mb-5 pb-5" v-if="(tvs != '')">
        <div class="row cont-card mx-auto">
            <h3 >Lista Serie Tv:</h3>

            <div v-for="element in tvs" :key="element.id" class="img-card-size position-relative">
                <img :src="completePosterPathW342(element.poster_path)" :alt="element.title"
                    class="display-inline-block">
                <div class="position-absolute info pt-3 ps-3">
                    <ul>
                        <li><span class="fw-bolder">Titolo: </span>{{element.name}}</li>
                        <li><span class="fw-bolder">Titolo Originale: </span>{{ element.original_name }}</li>
                        <li><span class="fw-bolder">Voto: </span>{{ changeValueVote(element.vote_average) }}</li>
                        <li><span class="fw-bolder">Panoramica: </span>{{ element.overview }}</li>
                    </ul>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
export default {
methods: {
        completePosterPathW342(path) {
            if (path != null || path == "") {
                path = `https://image.tmdb.org/t/p/w342/${path}`;
            }
            else {
                path = "/defaultw-342.jpg";
            }
            return path;
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
        },
    },
    props: {
        tvs: Array,
    },
}
</script>

<style>

</style>