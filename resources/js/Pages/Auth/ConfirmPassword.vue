<script>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';

export default {
    components: {
        GuestLayout,
        Head,
    },
    data() {
        return {
            form: useForm({
                password: '',
            }),
        }
    },
    methods: {
        submit() {
            this.form.post(route('password.confirm'), {
                onFinish: () => this.form.reset(),
            });
        },
    },
}
</script>

<template>
    <GuestLayout>
        <Head title="Confirm Password" />

        <div class="card shadow-sm">
            <div class="card-header">Confirmar contraseña</div>
            <div class="card-body">
                <p class="text-muted mb-4">
                    Esta es una área segura de la aplicación. Por favor, confirma tu contraseña antes de continuar.
                </p>

                <form @submit.prevent="submit">
                    <div class="mb-3">
                        <label for="password" class="form-label">Password</label>
                        <input
                            id="password"
                            v-model="form.password"
                            type="password"
                            class="form-control"
                            :class="{ 'is-invalid': form.errors.password }"
                            required
                            autocomplete="current-password"
                            autofocus
                        />
                        <div v-if="form.errors.password" class="invalid-feedback">{{ form.errors.password }}</div>
                    </div>
                    <div class="d-flex justify-content-end mt-4">
                        <button type="submit" class="btn btn-primary" :disabled="form.processing">
                            <span v-if="form.processing" class="spinner-border spinner-border-sm me-2" />
                            Confirmar
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </GuestLayout>
</template>
