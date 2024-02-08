<script>
import axios from 'axios';
import { api } from './components/data/index'
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {
  name: 'App',
  data: () => ({
    //* Initialize empty arrays to store movie and TV show results
    movieResults: [],
    tvResults: [],
    basePosterPath: api.basePosterPath,
  }),
  components: { AppHeader, AppMain },
  methods: {
    handleSearch(searchQuery) {
      //* API call to search for movies
      axios.get(`${api.baseUri}/search/movie`, {
        params: {
          api_key: api.apiKey,
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
      axios.get(`${api.baseUri}/search/tv`, {
        params: {
          api_key: api.apiKey,
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
  <AppMain :movieResults="movieResults" :tvResults="tvResults" :basePosterPath="basePosterPath" />
</template>


<style lang="scss">
@use './assets/scss/style.scss';
</style>
