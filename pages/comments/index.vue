<template>
  <div class="comment-container">
    <div v-if="$fetchState.pending" class="loading">
      <h1>Loading...</h1>
    </div>
    <div v-else-if="$fetchState.error">
      <h1>Could not fetch comments! :(</h1>
    </div>
    <div v-else>
      <search-box @searchComments="searchComment"></search-box>
      <div class="comment-list">
        <comment-box v-for="item in filteredComments" :key="item.id" :comment="item"></comment-box>
      </div>
    </div>
  </div>
</template>
<script>
import {
  defineComponent,
  useFetch,
  ref,
  useContext,
  reactive,
  toRefs
} from "@nuxtjs/composition-api";
import CommentBox from "../../components/CommentBox";
import SearchBox from "../../components/SearchBox";

export default defineComponent({
  components: {
    commentBox: CommentBox,
    searchBox: SearchBox
  },
  setup() {
    const comments = ref();
    const state = reactive({
      filteredComments: []
    });

    const { $axios } = useContext();

    useFetch(async () => {
      const res = await $axios.get(
        "https://jsonplaceholder.typicode.com/comments"
      );
      comments.value = res.data;
      state.filteredComments = comments.value;
      console.log('1:', comments);
    });
    console.log('2:', comments);

    function searchComment(comment) {
      if (comment) {
        const nonCaseSensitiveText = comment.toLowerCase();

        state.filteredComments = comments.value.filter(
          item =>
            item.body.includes(nonCaseSensitiveText) ||
            item.name.includes(nonCaseSensitiveText) ||
            item.email.includes(nonCaseSensitiveText)
        );
      } else {
        state.filteredComments = comments.value;
      }
    }

    return { ...toRefs(state), searchComment };
  }
});
</script>
<style scoped>
.comment-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
</style>