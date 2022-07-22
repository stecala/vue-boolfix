<template>
    <div class="pt-4 container-fluid ps-4">
        <div class="row cont-card mx-auto">
            <h3 v-if="(films != '')">Lista dei film:</h3>

            <div v-for="element in films" :key="element.id" class="img-card-size">
                <img :src="completePosterPathW342(element.poster_path)" :alt="element.title"
                    class="display-inline-block">
            </div>
        </div>

    </div>
</template>

<script>
export default {
    components: {

    },
    data: function () {
        return {

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
    },
    props: {
        films: Array,
    },
    created() {
    }
}
</script>

<style lang="scss" scoped>
.cont-card {
    width: calc((342px * 4) + (10px * 4));
    .img-card-size {
        width: 342px;
        display: inline-block;
        margin-right: 10px;
        margin-top: 10px;
    }

}
</style>