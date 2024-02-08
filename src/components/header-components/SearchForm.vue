<script>
export default {
  name: 'SearchForm',
  data: () => ({
    //* Data property to store searched query
    searchQuery: ''
  }),
  methods: {
    //* Method triggered when form submitted
    submitForm() {
      //* Emit 'search' event with search query as payload
      this.$emit('search', this.searchQuery);
    }
  }
};
</script>

<template>
  <!-- Search form -->
  <form id="form" class="search-form" @submit.prevent="submitForm">
    <!-- Input field for entering search query -->
    <input v-model.trim="searchQuery" type="text" placeholder="Search..." class="search-input">
    <!-- Button form submit-->
    <button type="submit" class="search-button">Search</button>
  </form>
</template>

<style scoped>
.search-form {
  display: flex;
  align-items: center;
}

.search-input {
  width: 200px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 8px;
}

.search-button {
  padding: 8px 16px;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
</style>
