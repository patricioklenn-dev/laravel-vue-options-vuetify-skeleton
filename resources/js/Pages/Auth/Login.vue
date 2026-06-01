<script>
import GuestLayout from '@/Layouts/GuestLayout.vue'
import { useForm } from '@inertiajs/vue3'

export default {
    components: {
        GuestLayout,
    },
    data() {
        return {
            form: useForm({
                email: '',
                password: '',
                remember: false,
            }),
        }
    },
    methods: {
        submit() {
            this.form.post(route('login'))
        },
    },
}
</script>

<template>
    <GuestLayout>
        <div class="card shadow-sm">
            <div class="card-header">Iniciar sesión</div>
            <div class="card-body">
                <form @submit.prevent="submit">
                    <div class="mb-3">
                        <label for="email" class="form-label">Email</label>
                        <input
                            id="email"
                            v-model="form.email"
                            type="email"
                            class="form-control"
                            :class="{ 'is-invalid': form.errors.email }"
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
                        />
                        <div v-if="form.errors.password" class="invalid-feedback">{{ form.errors.password }}</div>
                    </div>
                    <div class="mb-3 form-check">
                        <input id="remember" v-model="form.remember" type="checkbox" class="form-check-input" />
                        <label for="remember" class="form-check-label">Recordarme</label>
                    </div>
                    <button type="submit" class="btn btn-primary w-100" :disabled="form.processing">
                        <span v-if="form.processing" class="spinner-border spinner-border-sm me-2" />
                        Entrar
                    </button>
                </form>
            </div>
        </div>
    </GuestLayout>
</template>
