<script>
export default {
    name: 'MovieResults',
    props: {
        movieResults: Array,
        basePosterPath: String,
        transformVote: Function,
    },
    methods: {
        getPosterStyle(posterPath) {
            return posterPath ? `url(${this.basePosterPath}${posterPath})` : `url(../../assets/placeholed.jpg)`;
        }
    }
};
</script>

<template>
    <!-- Movie Results Section -->
    <div id="movies" class="text-white text-center my-5" v-if="movieResults.length > 0">
        <h2>Movie Results:</h2>
        <div class="grid">
            <!-- Loop through movie results -->
            <div class="item border-4 mb-4" v-for="movie in movieResults" :key="movie.id">
                <div class="poster" :style="{ 'background-image': getPosterStyle(movie.poster_path) }">
                    <div class="info">
                        <div><strong>Title:</strong> {{ movie.title }}</div>
                        <div><strong>Original Title:</strong><br /> {{ movie.original_title }}</div>
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
    </div>
</template>

<style scoped lang="scss">
.grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;

    .item {
        width: calc(25% - 20px);
        margin: 10px;
    }

    .flag img {
        max-width: 20px;
    }

    .poster {
        width: 100%;
        height: 450px;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: center;
        position: relative;
        display: block;

        .info {
            position: absolute;
            top: 0;
            left: 0;
            background-color: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 50px 10px 10px 10px;
            width: 100%;
            height: 100%;
            opacity: 0;
            transition: opacity 0.3s ease;
        }

        &:hover .info {
            opacity: 1;
        }
    }
}
</style>

