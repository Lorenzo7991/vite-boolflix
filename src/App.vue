<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {
  name: 'App',
  data: () => ({
    movieResults: []
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
          console.log('API call error:', error);
        });
    }
  }
};
</script>

<template>
  <AppHeader @search="handleSearch" />
  <AppMain :movieResults="movieResults" />
</template>
<style lang="scss">
@use './assets/scss/style.scss';
</style>

