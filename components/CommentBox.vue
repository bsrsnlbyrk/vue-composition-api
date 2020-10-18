<template>
    <div class="comment-box">
        <div class="comment-box-header">
            <span class="name">{{ comment.name }}</span>
            <span class="email">{{ comment.email }}</span>
        </div>
        <span class="comment-box-body">{{ comment.body }}</span>
    </div>
</template>

<script>
export default {
    props: {
        comment: {
            type: Object,
            required: true
        }
    }
}
</script>

<style scoped>
.comment-box {
    background-color: #f8f8f8;
    margin: 2rem 2rem;
    padding: 1rem 1rem;
}
.comment-box-header {
    display: flex;
    justify-content: flex-start;
    align-items: flex-end;
}
.comment-box-header .name {
    color: #333;
    font-weight: 700;
    font-size: 1rem;
    margin-bottom: 1rem;
}
.comment-box-header .email {
    color: #b8b8b8;
    font-weight: 400;
    font-size: .75rem;
    margin-bottom: 1rem;
    margin-left: .5rem;
}
.comment-box-body {
    color: #333;
    font-weight: 500;
    font-size: 1rem;
}
</style>