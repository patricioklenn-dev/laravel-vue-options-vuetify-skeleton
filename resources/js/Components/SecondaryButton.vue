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
    },
}
</script>

<template>
    <button :type="type" class="btn btn-outline-secondary" :disabled="disabled">
        <slot />
    </button>
</template>
