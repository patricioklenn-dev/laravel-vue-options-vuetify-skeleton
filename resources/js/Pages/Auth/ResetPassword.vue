<script>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';

export default {
    components: {
        GuestLayout,
        Head,
    },
    props: {
        email: {
            type: String,
            required: true,
        },
        token: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
            form: useForm({
                token: '',
                email: '',
                password: '',
                password_confirmation: '',
            }),
        }
    },
    created() {
        this.form.token = this.token;
        this.form.email = this.email;
    },
    methods: {
        submit() {
            this.form.post(route('password.store'), {
                onFinish: () => this.form.reset('password', 'password_confirmation'),
            });
        },
    },
}
</script>

<template>
    <GuestLayout>
        <Head title="Reset Password" />

        <div class="card shadow-sm">
            <div class="card-header">Restablecer contraseña</div>
            <div class="card-body">
                <form @submit.prevent="submit">
                    <div class="mb-3">
                        <label for="email" class="form-label">Correo electrónico</label>
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
                    <div class="mb-3">
                        <label for="password" class="form-label">Contraseña</label>
                        <input
                            id="password"
                            v-model="form.password"
                            type="password"
                            class="form-control"
                            :class="{ 'is-invalid': form.errors.password }"
                            required
                            autocomplete="new-password"
                        />
                        <div v-if="form.errors.password" class="invalid-feedback">{{ form.errors.password }}</div>
                    </div>
                    <div class="mb-3">
                        <label for="password_confirmation" class="form-label">Confirmar contraseña</label>
                        <input
                            id="password_confirmation"
                            v-model="form.password_confirmation"
                            type="password"
                            class="form-control"
                            :class="{ 'is-invalid': form.errors.password_confirmation }"
                            required
                            autocomplete="new-password"
                        />
                        <div v-if="form.errors.password_confirmation" class="invalid-feedback">{{ form.errors.password_confirmation }}</div>
                    </div>
                    <div class="d-flex justify-content-end mt-4">
                        <button type="submit" class="btn btn-primary" :disabled="form.processing">
                            <span v-if="form.processing" class="spinner-border spinner-border-sm me-2" />
                            Restablecer contraseña
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </GuestLayout>
</template>
