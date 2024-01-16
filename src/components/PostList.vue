<template>
  <div class="posts">
    <PostCard v-for="post in posts" :post="post" :key="post.id"/>
  </div>
</template>

<script lang="ts">
import { PropType, defineComponent } from 'vue';
import PostCard from './PostCard.vue';
import Post from '@/interfaces/post';

export default defineComponent({
  name: 'PostList',
  components: {
    PostCard
  },
  props: {
    posts: {
      required: true,
      type: Array as PropType<Post[]>
    }
  },
});
</script>

<style scoped>
  .posts {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }
</style>
