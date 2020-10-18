<template>
    <div class="search-box">
        <input type="text" placeholder="Search via words, user email or post id" v-model="searchedComment" @keyup.enter="search"/>
    </div>
</template>

<script>
import { defineComponent, reactive, toRefs } from '@nuxtjs/composition-api';

export default defineComponent({
    setup() {
        const state = reactive({
            searchedComment: null
        });

        function search() {
            console.log(state.searchedComment);
        }

        return { ...toRefs(state), search }
    }
})
</script>