<script>
export default {
  name: 'SearchForm',
  data: () => ({
    searchQuery: ''
  }),
  methods: {
    submitForm() {
      this.$emit('search', this.searchQuery);
    }
  }
};
</script>

<template>
  <form id="form" class="search-form" @submit.prevent="submitForm">
    <input v-model="searchQuery" type="text" placeholder="Search..." class="search-input">
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
