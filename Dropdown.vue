<template>
    <div class="container">
        <select
            name="options"
            id="options"
            class="w-100"
            :value="value"
            v-on:input="$emit('input', $event.target.value)"
        >
            <option
                v-for="(option, index) in options"
                :key="index"
                :value="option"
            >
                {{ option }}
            </option>
        </select>
    </div>
</template>

<script>
export default {
    props: {
        value: {
            type: String,
        },
        options: {
            type: Array,
            require: true,
        },
        placeholder: {
            type: String,
        },
    },
    data() {
        return {};
    },
};
</script>
