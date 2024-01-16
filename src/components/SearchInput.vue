<template lang="">
    <div class="search-wrapper">
        <input @input="emitSearch" type="text" name="search" placeholder="Search by title..." v-model="searchQuery">
    </div>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'SearchInput',
  setup(props, { emit }){
    const searchQuery = ref("");

    const emitSearch = () => {
        emit('search', searchQuery.value)
    }

    return {searchQuery, emitSearch}
  }
});
</script>
<style>
    .search-wrapper {
        width: 800px;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: 20px;
    }
    .search-wrapper input {
        width: 100%;
    }
</style>