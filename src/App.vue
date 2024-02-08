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
  }),
  components: { AppHeader, AppMain },
  methods: {
    handleSearch(searchQuery) {
      //* Promise.all to execute both API calls simultaneously
      Promise.all([
        axios.get(`${api.baseUri}/search/movie`, {
          params: {
            api_key: api.apiKey,
            query: searchQuery
          }
        }),
        axios.get(`${api.baseUri}/search/tv`, {
          params: {
            api_key: api.apiKey,
            query: searchQuery
          }
        })
      ])
        .then(([movieResponse, tvResponse]) => {
          //* Store movie and TV show results
          this.movieResults = movieResponse.data.results;
          this.tvResults = tvResponse.data.results;
        })
        .catch(error => {
          //* Log error if API call fails //TODO: manage errors
          console.log('API call error:', error);
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
