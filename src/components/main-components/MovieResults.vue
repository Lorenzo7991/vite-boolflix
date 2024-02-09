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
    <div id="movies" class="text-white text-center my-5" v-if="movieResults.length > 0">
        <h2>Movie Results:</h2>
        <div class="movies-grid">
            <!-- Loop through movie results -->
            <div class="movie-item" v-for="movie in movieResults" :key="movie.id">
                <div class="poster" v-bind:style="{ 'background-image': `url(${basePosterPath}${movie.poster_path})` }">
                    <div><strong>Title:</strong> {{ movie.title }}</div>
                    <div><strong>Original Title:</strong> {{ movie.original_title }}</div>
                    <!-- Display Italian flag if original language is Italian -->
                    <div class="flag" v-if="movie.original_language === 'it'">
                        <img src="@/assets/img/it.png" alt="Italian Flag Image">
                    </div>
                    <!-- Display English flag if original language is English -->
                    <div class="flag" v-else-if="movie.original_language === 'en'">
                        <img src="@/assets/img/en.png" alt="English Flag Image">
                    </div>
                    <div v-else>
                        <span><strong>Language:</strong><br />{{ movie.original_language }}</span>
                    </div>
                    <div><strong>Vote Average:</strong><br /> <span v-html="transformVote(movie.vote_average)"></span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
<style scoped>
.movies-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}

.movie-item {
    width: calc(25% - 20px);
    margin: 10px;
    border: 1px solid #ccc;
}

.flag img {
    max-width: 20px;
}

.poster {
    width: 100%;
    height: 400px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;

}
</style>
  