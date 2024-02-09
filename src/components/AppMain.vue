<script>
import MovieResults from './main-components/MovieResults.vue';
import TvShowResults from './main-components/TvShowsResults.vue';


export default {
    name: 'AppMain',
    components: { MovieResults, TvShowResults },
    props: {
        //* Props for movie results
        movieResults: {
            type: Array,
        },
        //* Props for TV show results
        tvResults: {
            type: Array
        },
        basePosterPath: {
            type: String
        }
    },
    methods: {
        //* Function to transform the vote average to stars
        transformVote(voteAverage) {
            //*Calculate number of full stars
            let fullStars = Math.round(voteAverage / 2);
            //* Create string containing star icons
            let starsHTML = '';
            for (let i = 0; i < fullStars; i++) {
                starsHTML += '<i class="fas fa-star"></i>';
            }
            //* Add empty stars to reach total of 5 stars
            for (let i = fullStars; i < 5; i++) {
                starsHTML += '<i class="far fa-star"></i>';
            }
            //* Return the HTML string containing the stars
            return starsHTML;
        }
    }

};
</script>


<template>
    <div id="container" class="container">
        <MovieResults :movieResults="movieResults" :basePosterPath="basePosterPath" :transformVote="transformVote" />
        <TvShowResults :tvResults="tvResults" :basePosterPath="basePosterPath" :transformVote="transformVote" />
    </div>
</template>


<style>
#ita-flag img {
    max-height: 20px;
    max-width: 50px;
    margin: 15px 0;
}

#eng-flag img {
    max-height: 20px;
    max-width: 50px;
    margin: 15px 0;
}
</style>
