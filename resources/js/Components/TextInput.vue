<script>
export default {
    props: {
        modelValue: {
            type: String,
            required: true,
        },
    },
    emits: ['update:modelValue'],
    mounted() {
        if (this.$refs.input?.$el?.hasAttribute('autofocus')) {
            this.$refs.input.$el.focus();
        }
    },
    methods: {
        focus() {
            this.$refs.input?.$el?.focus();
        },
    },
}
</script>

<template>
    <v-text-field
        :model-value="modelValue"
        @update:model-value="$emit('update:modelValue', $event)"
        ref="input"
    />
</template>
