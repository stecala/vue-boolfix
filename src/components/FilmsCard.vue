<template>
    <div class="pt-4 container-fluid ps-4 mb-5 pb-5 " v-if="(films != '')">
        <div class="row cont-card mx-auto">
            <h3>Lista dei film:</h3>

            <div v-for="element in films" :key="element.id" class="img-card-size position-relative">
                <img :src="completePosterPathW342(element.poster_path)" :alt="element.title"
                    class="display-inline-block">
                <div class="position-absolute info pt-3 ps-3">
                    <ul>
                        <li><span class="fw-bolder">Titolo Originale: </span>{{ element.original_title }}</li>
                        <li><span class="fw-bolder">Voto: </span>{{ changeValueVote(element.vote_average) }}</li>
                        <li><span class="fw-bolder">Panoramica: </span>{{ element.overview }}</li>
                    </ul>
                </div>
                <div class="position-absolute arrow-info" v-if="(isActive == false)" @click="changeStatusActive()">
                    <i class="fa-solid fa-angle-left"></i>
                </div>
                <div class="position-absolute arrow-info-active" v-else @click="changeStatusActive()">
                    <i class="fa-solid fa-angle-right"></i>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import axios from 'axios';
export default {
    data: function () {
        return {
            apiLink: 'https://api.themoviedb.org/3/movie/',
            apiKey: '/credits?api_key=290ef3b32debba72662776b92b209938',
            isActive: false,
        }
    },
    components: {

    },
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
        getCreditsMovie(id) {
            axios.get(this.apiLink + id + this.apiKey)
        },
        changeStatusActive() {
            this.isActive = !this.isActive
        }
    },
    props: {
        films: Array,
    },
    created() {
    }
}
</script>

<style lang="scss" >
@import '../assets/style/variable.scss';

.cont-card {
    max-width: calc((342px * 4) + (10px * 4));

    .img-card-size {
        width: 342px;
        display: inline-block;
        margin-right: 10px;
        margin-top: 10px;

        img {
            max-width: 342px;
            min-height: 513px;
        }

        .info {
            width: 100%;
            bottom: 0;
            left: 12px;
            background-color: rgba(0, 0, 0, 0.8);
            visibility: hidden;
            text-shadow: 2px 2px black;

            ul {
                padding-left: 0;
                list-style: none;
            }

        }

        &:hover {
            transition: 0.5s ease-in-out;
            transform: scale(1.2);
            z-index: 1;

            .info {
                visibility: visible;
            }
        }

        .arrow-info {
            width: 30px;
            height: 30px;
            background-color: rgba(0, 0, 0, 0.8);
            border-radius: 50%;
            font-size: 1rem;
            top: 10px;
            right: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            visibility: hidden;
            cursor: pointer;
        }

        &:hover .arrow-info {
            visibility: visible;
        }

        .arrow-info-active {
            width: 30px;
            height: 30px;
            background-color: black;
            color: red;
            border-radius: 50%;
            font-size: 1rem;
            top: 10px;
            right: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
            visibility: hidden;
            cursor: pointer;
        }

    }

}
</style>