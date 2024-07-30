<template>
    <div class="container">
        <div class="row justify-content-center">
            <input
                placeholder="Add a comment"
                class="mt-2"
                :value="value"
                v-on:input="$emit('input', $event.target.value)"
            />
        </div>
        <div class="text-center">
            <button class="mt-2 m-auto" @click="$emit('add-comment')">
                Save
            </button>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: {
            type: String,
        },
    },
};
</script>
