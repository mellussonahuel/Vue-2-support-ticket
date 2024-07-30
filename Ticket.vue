<template>
    <div class="d-flex flex-column p-2 m-auto">
        <p><strong>Subject:</strong> {{ ticket.subject }}</p>
        <p><strong>Description:</strong> {{ ticket.description }}</p>
        <div class="d-flex justify-between">
            <p><strong>Status:</strong> {{ ticket.status }}</p>
            <span class="d-block">
                <slot></slot>
            </span>
        </div>
        <CommentsLists :comments="ticket.comments" />
    </div>
</template>

<script>
import CommentsLists from "./CommentsLists.vue";
export default {
    props: {
        ticket: {
            type: Object,
            required: true,
        },
    },
    components: {
        CommentsLists,
    },
};
</script>
