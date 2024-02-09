<script>
export default {
    name: 'TvShowResults',
    props: {
        tvResults: Array,
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
    <!-- TV Show Results Section -->
    <div id="tv-series" class="text-white text-center my-5" v-if="tvResults.length > 0">
        <h2>TV Show Results:</h2>
        <div class="grid">
            <!-- Loop through TV show results -->
            <div class="item border-4 mb-4" v-for="show in tvResults" :key="show.id">
                <div class="poster" v-bind:style="{ 'background-image': getPosterStyle(show.poster_path) }">
                    <div class="info">
                        <div><strong>Title:</strong> {{ show.name }}</div>
                        <div><strong>Original Title:</strong><br /> {{ show.original_name }}</div>
                        <!-- Display Italian flag if original language is Italian -->
                        <div class="flag" v-if="show.original_language === 'it'">
                            <img src="@/assets/img/it.png" alt="Italian Flag Image">
                        </div>
                        <!-- Display English flag if original language is English -->
                        <div class="flag" v-else-if="show.original_language === 'en'">
                            <img src="@/assets/img/en.png" alt="English Flag Image">
                        </div>
                        <div v-else>
                            <span><strong>Language:</strong><br /> {{ show.original_language }}</span>
                        </div>
                        <div><strong>Vote Average:</strong><br /> <span v-html="transformVote(show.vote_average)"></span>
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

