<script>
export default {
    name: 'MovieResults',
    data: () => ({}),
    props: {
        movieResults: Array,
        basePosterPath: String,
        transformVote: Function,
    },
};
</script>

<template>
    <!-- Movie Results Section -->
    <div id="movies" class="text-white my-5 " v-if="movieResults.length > 0">
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
                <div><strong>Vote Average:</strong> <span v-html="transformVote(movie.vote_average)"></span></div>
            </li>
        </ul>
    </div>
</template>
