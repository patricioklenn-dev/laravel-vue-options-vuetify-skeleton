<script>
export default {
    props: {
        value: {
            type: String,
        },
        for: {
            type: String,
        },
    },
}
</script>

<template>
    <label class="form-label" :for="for">
        <span v-if="value">{{ value }}</span>
        <span v-else><slot /></span>
    </label>
</template>
