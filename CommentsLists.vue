<template>
    <div class="container">
        <div class="row justify-content-center">
            <ul v-if="comments.length">
                <li v-for="(comment, index) in comments" :key="index">
                    {{ comment }}
                </li>
            </ul>
            <P v-else class="text-center m-auto"> No comments yet</P>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        comments: {
            type: Array,
        },
    },
};
</script>
