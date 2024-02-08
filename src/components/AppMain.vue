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
        //* Method to transform vote average from decimal to a range from 1 to 5, rounding up
        transformVote(voteAverage) {
            let transformedVote = Math.ceil(voteAverage * 5);
            transformedVote = Math.min(transformedVote, 5);
            transformedVote = Math.max(transformedVote, 1);
            return transformedVote;
        }
    }
};
</script>


<template>
    <div id="temporary-container" class="container">

        <!-- Movie Results Section -->
        <div id="movies" class="text-white my-5">
            <h2>Movie Results:</h2>
            <ul>
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
                    <div><strong>Vote Average:</strong> {{ transformVote(movie.vote_average) }}</div>
                </li>
            </ul>
        </div>

        <!-- TV Show Results Section -->
        <div id="tv-series" class="text-white">
            <h2>TV Show Results:</h2>
            <ul>
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
                    <div><strong>Vote Average:</strong> {{ transformVote(show.vote_average) }}</div>
                </li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
#ita-flag img {
    max-height: 20px;
    max-width: 50px;
}

#eng-flag img {
    max-height: 20px;
    max-width: 50px;
}
</style>
