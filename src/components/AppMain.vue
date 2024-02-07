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
                    <!-- Display generic icon if neither Italian nor English -->
                    <div v-else>
                        <span><i class="fa-solid fa-language fa-2x"></i></span>
                    </div>
                    <div><strong>Vote Average:</strong> {{ movie.vote_average }}</div>
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
                    <!-- Display generic icon if neither Italian nor English -->
                    <div v-else>
                        <span><i class="fa-solid fa-language fa-2x"></i></span>
                    </div>
                    <div><strong>Vote Average:</strong> {{ show.vote_average }}</div>
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
