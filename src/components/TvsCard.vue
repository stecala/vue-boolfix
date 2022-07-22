<template>
    <div class="pt-4 container-fluid ps-4 mb-5 pb-5" v-if="(tvs != '')">
        <div class="row cont-card mx-auto">
            <h3>Lista Serie Tv:</h3>

            <div v-for="element in tvs" :key="element.id" class="img-card-size position-relative" @mouseleave="setFalseToIsActive()">
                <img :src="completePosterPathW342(element.poster_path)" :alt="element.title">
                <div class="position-absolute info pt-3 ps-3">
                    <ul>
                        <li><span class="fw-bolder">Titolo Originale: </span>{{ element.original_name }}</li>
                        <li><span class="fw-bolder">Voto: </span>{{ changeValueVote(element.vote_average) }}</li>
                        <li><span class="fw-bolder">Panoramica: </span>{{ element.overview }}</li>
                    </ul>
                </div>
                <div class="position-absolute arrow-info" v-if="(isActive == false)"
                    @click="changeStatusActive() ; getCreditsTvs(element.id)">
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
            apiLink: 'https://api.themoviedb.org/3/tv/',
            apiKey: '/credits?api_key=290ef3b32debba72662776b92b209938',
            isActive: false,
            creditsList: [],
        }
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
        getCreditsTvs(id){
            this.creditsList = []
            axios.get(this.apiLink + id + this.apiKey)
                .then((result)=> {
                    this.creditsList = result.data.cast
                    this.creditsList.splice(5)
                    console.log(this.creditsList)
                })
            .catch((error)=>{
                console.warn(error)
            })
        },
        changeStatusActive(){
            this.isActive = !this.isActive
        },
        setFalseToIsActive(){
            this.isActive = false
        },
        mapGenres(id){
            console.log(this.tvsGenreList)
            return this.tvsGenreList.find(element => element.id == id).name
        }
    },
    props: {
        tvs: Array,
        tvsGenreList: Array,
    },
}
</script>

<style>
</style>