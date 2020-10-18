<template>
    <div class="comment-container">
        <div v-if="$fetchState.pending" class="loading">
            <h1>Loading...</h1>
        </div>
        <div v-else-if="$fetchState.error">
            <h1>Could not fetch comments! :(</h1>
        </div>
        <div v-else>
            <search-box></search-box>
            <div class="comment-list">
                <comment-box v-for="item in comments" :key="item.id" :comment="item" ></comment-box>
            </div>
        </div>
    </div>
</template>
<script>
import { defineComponent, useFetch, ref, useContext } from '@nuxtjs/composition-api';
import CommentBox from '../../components/CommentBox';
import SearchBox from '../../components/SearchBox';

export default defineComponent({
    components: {
        commentBox: CommentBox,
        searchBox: SearchBox
    },
    setup() {
        const comments = ref();

        const { $axios } = useContext();
        
        useFetch(async () => {
            const res = await $axios.get('https://jsonplaceholder.typicode.com/comments');
            comments.value = res.data;
        });

        return { comments }
    }
})
</script>
<style scoped>
.comment-list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
}
</style>