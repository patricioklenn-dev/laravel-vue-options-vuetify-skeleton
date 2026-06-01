<script>
import { useForm } from '@inertiajs/vue3';

export default {
    data() {
        return {
            form: useForm({
                current_password: '',
                password: '',
                password_confirmation: '',
            }),
        }
    },
    methods: {
        updatePassword() {
            this.form.put(route('password.update'), {
                preserveScroll: true,
                onSuccess: () => this.form.reset(),
                onError: () => {
                    if (this.form.errors.password) {
                        this.form.reset('password', 'password_confirmation');
                        this.$refs.passwordInput.focus();
                    }
                    if (this.form.errors.current_password) {
                        this.form.reset('current_password');
                        this.$refs.currentPasswordInput.focus();
                    }
                },
            });
        },
    },
}
</script>

<template>
    <section>
        <header class="mb-4">
            <h2 class="h5 mb-2">Actualizar contraseña</h2>
            <p class="text-muted small mb-0">
                Asegura que tu cuenta esté usando una contraseña larga y aleatoria para mantenerse segura.
            </p>
        </header>

        <form @submit.prevent="updatePassword">
            <div class="mb-3">
                <label for="current_password" class="form-label">Contraseña actual</label>
                <input
                    id="current_password"
                    ref="currentPasswordInput"
                    v-model="form.current_password"
                    type="password"
                    class="form-control"
                    :class="{ 'is-invalid': form.errors.current_password }"
                    autocomplete="current-password"
                />
                <div v-if="form.errors.current_password" class="invalid-feedback">{{ form.errors.current_password }}</div>
            </div>
            <div class="mb-3">
                <label for="password" class="form-label">Nueva contraseña</label>
                <input
                    id="password"
                    ref="passwordInput"
                    v-model="form.password"
                    type="password"
                    class="form-control"
                    :class="{ 'is-invalid': form.errors.password }"
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
                    autocomplete="new-password"
                />
                <div v-if="form.errors.password_confirmation" class="invalid-feedback">{{ form.errors.password_confirmation }}</div>
            </div>

            <div class="d-flex align-items-center gap-3 mt-4">
                <button type="submit" class="btn btn-primary" :disabled="form.processing">
                    <span v-if="form.processing" class="spinner-border spinner-border-sm me-2" />
                    Guardar
                </button>
                <span v-if="form.recentlySuccessful" class="small text-muted">Guardado.</span>
            </div>
        </form>
    </section>
</template>
