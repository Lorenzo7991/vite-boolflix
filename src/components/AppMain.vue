<script>
export default {
    name: 'AppMain',
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
            //* Log the HTML string containing the stars
            console.log(starsHTML);
            //* Return the HTML string containing the stars
            return starsHTML;
        }
    }

};
</script>


<template>
    <div id="temporary-container" class="container">

        <!-- Movie Results Section -->
        <div id="movies" class="text-white my-5">
            <h2>Movie Results:</h2>
            <!-- Move v-for to ul -->
            <ul v-if="movieResults.length">
                <!-- Loop through movie results -->
                <li class="border-bottom border-4 mb-4" v-for="movie in movieResults" :key="movie.id">
                    <div><strong>Title:</strong> {{ movie.title }}</div>
                    <div><strong>Original Title:</strong> {{ movie.original_title }}</div>
                    <!-- Display Italian flag if original language is Italian -->
                    <div id="ita-flag" v-if="movie.original_language === 'it'">
                        <img src="@/assets/img/it.png" alt="Italian Flag Image">
                    </div>
                    <!-- Display English flag if original language is English -->
                    <div id="eng-flag" v-else-if="movie.original_language === 'en'">
                        <img src="@/assets/img/en.png" alt="English Flag Image">
                    </div>
                    <div v-else>
                        <span><strong>Language:</strong> {{ movie.original_language }}</span>
                    </div>
                    <img v-if="movie.poster_path" :src="`${basePosterPath}${movie.poster_path}`" alt="Movie Poster">
                    <!-- Display placeholder image if poster_path is not present -->
                    <img v-else src="@/assets/img/placeholder.jpg" alt="Placeholder Image">
                    <div><strong>Vote Average:</strong> <span v-html="transformVote(movie.vote_average)"></span></div>
                </li>
            </ul>
        </div>

        <!-- TV Show Results Section -->
        <div id="tv-series" class="text-white">
            <h2>TV Show Results:</h2>
            <!-- Move v-for to ul -->
            <ul v-if="tvResults.length">
                <!-- Loop through TV show results -->
                <li class="border-bottom border-4 mb-4" v-for="show in tvResults" :key="show.id">
                    <div><strong>Title:</strong> {{ show.name }}</div>
                    <div><strong>Original Title:</strong> {{ show.original_name }}</div>
                    <!-- Display Italian flag if original language is Italian -->
                    <div id="ita-flag" v-if="show.original_language === 'it'">
                        <img src="@/assets/img/it.png" alt="Italian Flag Image">
                    </div>
                    <!-- Display English flag if original language is English -->
                    <div id="eng-flag" v-else-if="show.original_language === 'en'">
                        <img src="@/assets/img/en.png" alt="English Flag Image">
                    </div>
                    <div v-else>
                        <span><strong>Language:</strong> {{ show.original_language }}</span>
                    </div>
                    <!-- Display TV show poster if poster_path is present -->
                    <img v-if="show.poster_path" :src="`${basePosterPath}${show.poster_path}`" alt="TV Show Poster">
                    <!-- Display placeholder image if poster_path is not present -->
                    <img v-else src="@/assets/img/placeholder.jpg" alt="Placeholder Image">
                    <div><strong>Vote Average:</strong> <span v-html="transformVote(show.vote_average)"></span></div>
                </li>
            </ul>
        </div>
    </div>
</template>


<style scoped>
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
