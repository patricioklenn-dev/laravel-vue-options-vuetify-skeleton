<script>
export default {
    props: {
        modelValue: {
            type: String,
            required: true,
        },
        error: {
            type: String,
            default: '',
        },
    },
    emits: ['update:modelValue'],
    mounted() {
        if (this.$refs.input?.hasAttribute('autofocus')) {
            this.$refs.input.focus();
        }
    },
    methods: {
        focus() {
            this.$refs.input?.focus();
        },
    },
}
</script>

<template>
    <input
        ref="input"
        :value="modelValue"
        class="form-control"
        :class="{ 'is-invalid': error }"
        @input="$emit('update:modelValue', $event.target.value)"
    />
    <div v-if="error" class="invalid-feedback">{{ error }}</div>
</template>
