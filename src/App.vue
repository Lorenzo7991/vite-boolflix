<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {
  name: 'App',
  data: () => ({
    movieResults: [],
    tvResults: [],
  }),
  components: { AppHeader, AppMain },
  methods: {
    handleSearch(searchQuery) {
      axios
        .get('https://api.themoviedb.org/3/search/movie', {
          params: {
            api_key: 'a3cc6271bb5f76a0046a2b13e276b54c',
            query: searchQuery
          }
        })
        .then(response => {
          this.movieResults = response.data.results;
        })
        .catch(error => {
          console.log('API call error for movies:', error);
        });

      axios
        .get('https://api.themoviedb.org/3/search/tv', {
          params: {
            api_key: 'a3cc6271bb5f76a0046a2b13e276b54c',
            query: searchQuery
          }
        })
        .then(response => {
          this.tvResults = response.data.results;
        })
        .catch(error => {
          console.log('API call error for TV shows:', error);
        });
    }
  }
};
</script>


<template>
  <AppHeader @search="handleSearch" />
  <AppMain :movieResults="movieResults" :tvResults="tvResults" />
</template>


<style lang="scss">
@use './assets/scss/style.scss';
</style>

