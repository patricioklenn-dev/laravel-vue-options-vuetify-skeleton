<script>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';

export default {
    components: {
        GuestLayout,
        Head,
    },
    props: {
        status: {
            type: String,
        },
    },
    data() {
        return {
            form: useForm({
                email: '',
            }),
        }
    },
    methods: {
        submit() {
            this.form.post(route('password.email'));
        },
    },
}
</script>

<template>
    <GuestLayout>
        <Head title="Forgot Password" />

        <div class="card shadow-sm">
            <div class="card-header">Forgot Password</div>
            <div class="card-body">
                <p class="text-muted mb-4">
                    Olvidaste tu contraseña? No hay problema. Simplemente dínos tu dirección de correo electrónico y te enviaremos un enlace de restablecimiento de contraseña que te permitirá elegir una nueva.
                </p>

                <div v-if="status" class="alert alert-success mb-4">{{ status }}</div>

                <form @submit.prevent="submit">
                    <div class="mb-3">
                        <label for="email" class="form-label">Email</label>
                        <input
                            id="email"
                            v-model="form.email"
                            type="email"
                            class="form-control"
                            :class="{ 'is-invalid': form.errors.email }"
                            required
                            autofocus
                            autocomplete="username"
                        />
                        <div v-if="form.errors.email" class="invalid-feedback">{{ form.errors.email }}</div>
                    </div>
                    <div class="d-flex justify-content-end mt-4">
                        <button type="submit" class="btn btn-primary" :disabled="form.processing">
                            <span v-if="form.processing" class="spinner-border spinner-border-sm me-2" />
                            Enviar enlace de restablecimiento de contraseña
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </GuestLayout>
</template>
