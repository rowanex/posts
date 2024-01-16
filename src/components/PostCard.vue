<template>
    <div class="post">
        <div class="post__title">
            {{ post.title }}
        </div>
    </div>
</template>
<script lang="ts">
import Post from '@/interfaces/post';
import { PropType, defineComponent } from 'vue';

export default defineComponent({
  name: 'PostCard',
  props: {
    post: {
        required: true,
        type: Object as PropType<Post>
    }
  },
});
</script>
<style>
    .post {
        padding: 10px;
        max-width: 1160px;
        background-color: lightgrey;
    }
</style>