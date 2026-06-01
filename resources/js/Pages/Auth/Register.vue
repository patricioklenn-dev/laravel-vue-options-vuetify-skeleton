<script>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

export default {
    components: {
        GuestLayout,
        Head,
        Link,
    },
    data() {
        return {
            form: useForm({
                name: '',
                email: '',
                password: '',
                password_confirmation: '',
            }),
        }
    },
    methods: {
        submit() {
            this.form.post(route('register'), {
                onFinish: () => this.form.reset('password', 'password_confirmation'),
            });
        },
    },
}
</script>

<template>
    <GuestLayout>
        <Head title="Register" />

        <div class="card shadow-sm">
            <div class="card-header">Registrar</div>
            <div class="card-body">
                <form @submit.prevent="submit">
                    <div class="mb-3">
                        <label for="name" class="form-label">Nombre</label>
                        <input
                            id="name"
                            v-model="form.name"
                            type="text"
                            class="form-control"
                            :class="{ 'is-invalid': form.errors.name }"
                            required
                            autofocus
                            autocomplete="name"
                        />
                        <div v-if="form.errors.name" class="invalid-feedback">{{ form.errors.name }}</div>
                    </div>
                    <div class="mb-3">
                        <label for="email" class="form-label">Correo electrónico</label>
                        <input
                            id="email"
                            v-model="form.email"
                            type="email"
                            class="form-control"
                            :class="{ 'is-invalid': form.errors.email }"
                            required
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
                    <div class="d-flex justify-content-between align-items-center mt-4">
                        <Link :href="route('login')" class="text-decoration-none">Ya tienes una cuenta?</Link>
                        <button type="submit" class="btn btn-primary" :disabled="form.processing">
                            <span v-if="form.processing" class="spinner-border spinner-border-sm me-2" />
                            Registrar
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </GuestLayout>
</template>
