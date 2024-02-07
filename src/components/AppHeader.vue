<script>
import HeaderTitle from './header-components/HeaderTitle.vue';
import SearchForm from './header-components/SearchForm.vue';

export default {
    name: 'AppHeader',
    components: { HeaderTitle, SearchForm },
    methods: {
        //* Method triggered when search form emit 'search' event
        submitForm(searchQuery) {
            //* Emit 'search' event with search query as payload
            this.$emit('search', searchQuery);
        }
    }
};
</script>

<template>
    <!-- Header section -->
    <header>
        <!-- Render HeaderTitle component -->
        <HeaderTitle />
        <!-- Render SearchForm component and listen for 'search' event -->
        <SearchForm @search="submitForm" />
    </header>
</template>

<style scoped>
header {
    position: fixed;
    top: 0;
    width: 100%;
    height: 100px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 1rem;
    background-color: black;
}
</style>
