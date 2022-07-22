<template>
    <div class="pt-4 container-fluid ps-4 mb-5 pb-5 " v-if="(films != '')">
        <div class="row cont-card mx-auto">
            <h3>Lista dei film:</h3>

            <div v-for="element in films" :key="element.id" class="img-card-size position-relative"
                @mouseleave="setFalseToIsActive() ; resetArray(creditsList) ; resetArray(movieGenreList)">
                <img :src="completePosterPathW342(element.poster_path)" :alt="element.title"
                    class="display-inline-block">
                <div class="position-absolute info pt-3 ps-3" v-if="(isActive == false)">
                    <ul>
                        <li><span class="fw-bolder">Titolo Originale: </span>{{ element.original_title }}</li>
                        <li><span class="fw-bolder">Voto: </span>{{ changeValueVote(element.vote_average) }}</li>
                        <li><span class="fw-bolder">Panoramica: </span>{{ element.overview }}</li>
                    </ul>
                </div>
                <div class="position-absolute arrow-info" v-if="(isActive == false)"
                    @click="changeStatusActive() ; getCreditsMovie(element.id)">
                    <i class="fa-solid fa-angle-left"></i>
                </div>
                <div class="position-absolute arrow-info-active" v-else @click="changeStatusActive()">
                    <i class="fa-solid fa-angle-right"></i>
                </div>
                <div class="credits-container position-absolute pt-3 ps-3" v-if="isActive">
                    <ul  class="my-padding">
                        <li>Cast:
                            <ul>
                                <li v-for="(name, index) in creditsList" :key="index">{{ creditsList[index].name }}</li>

                            </ul>
                        </li>
                    </ul>
                    <ul class="my-padding">
                        <li >Generi:
                            <ul>
                                <li v-for="(id, index) in element.genre_ids" :key="index">{{ mapGenres(id) }}</li>

                            </ul>
                        </li>
                    </ul>
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
            creditsList: [],
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
                .then((result) => {
                    this.creditsList = result.data.cast
                    this.creditsList.splice(5)
                })
                .catch((error) => {
                    console.warn(error)
                })
        },
        changeStatusActive() {
            this.isActive = !this.isActive
        },
        setFalseToIsActive() {
            this.isActive = false
        },
        resetArray(arrayToReset) {
            arrayToReset = []
            return arrayToReset
        },
        mapGenres(id) {
            return this.movieGenreList.find(element => element.id == id).name
        }
    },
    props: {
        films: Array,
        movieGenreList: Array,
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

        .arrow-info-active {
            width: 30px;
            height: 30px;
            z-index: 3;
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

        .credits-container {
            width: 100%;
            height: 100%;
            top: 0;
            left: 12px;
            background-color: rgba(0, 0, 0, 0.8);
            visibility: hidden;

            ul {
                list-style-type: none;

            }
        }

        &:hover .arrow-info,
        &:hover .arrow-info-active,
        &:hover .credits-container {
            visibility: visible;
        }
    }
    .my-padding{
        padding-left: 0;
    }
}
</style>