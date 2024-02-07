<script>
export default {
    name: 'AppMain',
    props: {
        movieResults: {
            type: Array,

        }
    }
};
</script>


<template>
    <div class="text-white">
        <h2>Movie Results:</h2>
        <ul>
            <li class="border-bottom border-4 mb-4" v-for="movie in movieResults" :key="movie.id">
                <div><strong>Title:</strong> {{ movie.title }}</div>
                <div><strong>Original Title:</strong> {{ movie.original_title }}</div>
                <div><strong>Language:</strong> {{ movie.original_language }}</div>
                <div><strong>Vote Average:</strong> {{ movie.vote_average }}</div>
            </li>
        </ul>
    </div>
</template>


<style scoped>
/* Style here */
</style>