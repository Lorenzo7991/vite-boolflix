<script>
export default {
    name: 'TvShowResults',
    props: {
        tvResults: Array,
        basePosterPath: String,
        transformVote: Function,
    },
};
</script>

<template>
    <!-- TV Show Results Section -->
    <div id="tv-series" class="text-white" v-if="tvResults.length > 0">
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
                <div><strong>Vote Average:</strong> <span v-html="transformVote(show.vote_average)"></span></div>
            </li>
        </ul>
    </div>
</template>


<style scoped>
/* Style here */
</style>
