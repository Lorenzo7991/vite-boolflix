<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {
  name: 'App',
  data: () => ({
    //** Initialize empty arrays to store movie and TV show results
    movieResults: [],
    tvResults: [],
  }),
  components: { AppHeader, AppMain },
  methods: {
    handleSearch(searchQuery) {
      //* API call to search for movies
      axios
        .get('https://api.themoviedb.org/3/search/movie', {
          params: {
            api_key: 'a3cc6271bb5f76a0046a2b13e276b54c',
            query: searchQuery
          }
        })
        .then(response => {
          //* Store movie results in data property
          this.movieResults = response.data.results;
        })
        .catch(error => {
          //* Log error if API call fails for movies //TODO: manage errors
          console.log('API call error for movies:', error);
        });

      //* API call to search for TV shows
      axios
        .get('https://api.themoviedb.org/3/search/tv', {
          params: {
            api_key: 'a3cc6271bb5f76a0046a2b13e276b54c',
            query: searchQuery
          }
        })
        .then(response => {
          //* Store TV show results in data property
          this.tvResults = response.data.results;
        })
        .catch(error => {
          //* Log error if API call fails for TV shows //TODO: manage errors
          console.log('API call error for TV shows:', error);
        });
    }
  }
};
</script>


<template>
  <!-- Render AppHeader component and pass handleSearch method as a prop -->
  <AppHeader @search="handleSearch" />
  <!-- Render AppMain component and pass movieResults and tvResults data as props -->
  <AppMain :movieResults="movieResults" :tvResults="tvResults" />
</template>


<style lang="scss">
@use './assets/scss/style.scss';
</style>
