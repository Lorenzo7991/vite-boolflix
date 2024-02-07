<script>
import HeaderTitle from './header-components/HeaderTitle.vue';
import SearchForm from './header-components/SearchForm.vue';

export default {
    name: 'AppHeader',
    components: { HeaderTitle, SearchForm },
    methods: {
        submitForm(searchQuery) {

            this.$emit('search', searchQuery);
        }
    }
};
</script>

<template>
    <header>
        <HeaderTitle />
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
