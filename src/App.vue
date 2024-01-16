<template>
  <SearchInput @search="handleSearch"/>
  <PostList :posts="searchedPosts" v-if="!isPostsLoading" />
  <LoadingScreen v-else/>
</template>

<script lang="ts">
import { computed, defineComponent, onMounted, ref } from 'vue';
import PostList from './components/PostList.vue';
import LoadingScreen from './components/LoadingScreen.vue';
import SearchInput from './components/SearchInput.vue';
import Post from '@/interfaces/post'

export default defineComponent({
  name: 'App',
  components: {
    PostList,
    LoadingScreen,
    SearchInput
  },
  setup() {

    const posts = ref<Post[]>([])
    const isPostsLoading = ref(true);
    const searchQuery = ref("");

    const fetchPosts = async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        if (!response.ok){
          console.error(`Fetch error. ${response.status} Text: ${response.statusText}`)
        }
        posts.value = await response.json();
      } catch(error) {
        console.error(`Fetch error. ${error}`)
      } finally {
        isPostsLoading.value = false;
      }
    }

    const handleSearch = (newSearhQuery: string) => {
      searchQuery.value = newSearhQuery;

    }

    const searchedPosts = computed(() => {
      return posts.value.filter((post) =>
        post.title.toLowerCase().includes(searchQuery.value.toLowerCase())
      )
    });

    onMounted(fetchPosts);

    return {searchedPosts, isPostsLoading, handleSearch }
  }
});
</script>

<style>
  #app {
    max-width: 1160px;
    margin-left: auto;
    margin-right: auto;
    margin-top: 30px;
  }
</style>
