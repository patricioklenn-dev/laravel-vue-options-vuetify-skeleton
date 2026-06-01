<script>
export default {
    props: {
        show: {
            type: Boolean,
            default: false,
        },
        closeable: {
            type: Boolean,
            default: true,
        },
    },
    emits: ['close'],
    methods: {
        handleClose() {
            if (this.closeable) {
                this.$emit('close');
            }
        },
    },
}
</script>

<template>
    <template v-if="show">
        <div class="modal fade show d-block" tabindex="-1" @click.self="handleClose">
            <div class="modal-dialog">
                <slot />
            </div>
        </div>
        <div class="modal-backdrop fade show" />
    </template>
</template>
