<template>
    <div class="search-box">
        <input type="text" placeholder="Search via words, user email or post id" v-model="searchedComment" @keyup.enter="search"/>
    </div>
</template>

<script>
import { defineComponent, reactive, toRefs, useContext } from '@nuxtjs/composition-api';

export default defineComponent({
    name: 'SearchBox',
    setup(props, { emit }) {
        const state = reactive({
            searchedComment: null
        });

        function search() {
            emit('searchComments', state.searchedComment);
        }

        return { ...toRefs(state), search }
    }
})
</script>

<style scoped>
.search-box {
    width: 35%;
    padding: 1.5rem 2rem;
}
input {
    width: 100%;
    height: 2rem;
    border: 1px solid #b8b8b8;
    border-radius: 3px;
}
</style>