<script>
export default {
    props: {
        type: {
            type: String,
            default: 'button',
        },
        disabled: {
            type: Boolean,
            default: false,
        },
        loading: {
            type: Boolean,
            default: false,
        },
    },
}
</script>

<template>
    <button :type="type" class="btn btn-danger" :disabled="disabled || loading">
        <span v-if="loading" class="spinner-border spinner-border-sm me-2" />
        <slot />
    </button>
</template>
