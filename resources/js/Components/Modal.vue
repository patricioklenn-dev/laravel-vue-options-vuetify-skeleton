<script>
export default {
    props: {
        show: {
            type: Boolean,
            default: false,
        },
        maxWidth: {
            type: String,
            default: '2xl',
        },
        closeable: {
            type: Boolean,
            default: true,
        },
    },
    emits: ['close'],
    computed: {
        maxWidthValue() {
            const mapping = {
                sm: '400',
                md: '500',
                lg: '600',
                xl: '700',
                '2xl': '800',
            };
            return mapping[this.maxWidth] || '800';
        },
    },
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
    <v-dialog
        :model-value="show"
        :max-width="maxWidthValue"
        @update:model-value="(val) => !val && handleClose()"
        :persistent="!closeable"
    >
        <slot v-if="show" />
    </v-dialog>
</template>
