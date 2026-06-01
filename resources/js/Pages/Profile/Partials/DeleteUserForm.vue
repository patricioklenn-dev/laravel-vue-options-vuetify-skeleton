<script>
import { useForm } from '@inertiajs/vue3';

export default {
    data() {
        return {
            confirmingUserDeletion: false,
            form: useForm({
                password: '',
            }),
        }
    },
    methods: {
        confirmUserDeletion() {
            this.confirmingUserDeletion = true;
            this.$nextTick(() => this.$refs.passwordInput.focus());
        },
        deleteUser() {
            this.form.delete(route('profile.destroy'), {
                preserveScroll: true,
                onSuccess: () => this.closeModal(),
                onError: () => this.$refs.passwordInput.focus(),
                onFinish: () => this.form.reset(),
            });
        },
        closeModal() {
            this.confirmingUserDeletion = false;
            this.form.reset();
        },
    },
}
</script>

<template>
    <section>
        <header class="mb-4">
            <h2 class="h5 mb-2">Eliminar cuenta</h2>
            <p class="text-muted small mb-0">
                Una vez que se elimine tu cuenta, todos sus recursos y datos se eliminarán permanentemente. Antes de eliminar
                tu cuenta, por favor descarga cualquier dato o información que desees conservar.
            </p>
        </header>

        <button type="button" class="btn btn-danger" @click="confirmUserDeletion">Eliminar cuenta</button>

        <template v-if="confirmingUserDeletion">
            <div class="modal fade show d-block" tabindex="-1" @click.self="closeModal">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h5 class="modal-title">¿Estás seguro de querer eliminar tu cuenta?</h5>
                            <button type="button" class="btn-close" @click="closeModal" />
                        </div>
                        <div class="modal-body">
                            <p class="text-muted small mb-3">
                                Una vez que se elimine tu cuenta, todos sus recursos y datos se eliminarán permanentemente. Por favor
                                ingresa tu contraseña para confirmar que deseas eliminar tu cuenta permanentemente.
                            </p>
                            <div class="mb-3">
                                <label for="delete_password" class="form-label">Contraseña</label>
                                <input
                                    id="delete_password"
                                    ref="passwordInput"
                                    v-model="form.password"
                                    type="password"
                                    class="form-control"
                                    :class="{ 'is-invalid': form.errors.password }"
                                    placeholder="Contraseña"
                                    @keyup.enter="deleteUser"
                                />
                                <div v-if="form.errors.password" class="invalid-feedback">{{ form.errors.password }}</div>
                            </div>
                        </div>
                        <div class="modal-footer">
                            <button type="button" class="btn btn-secondary" @click="closeModal">Cancelar</button>
                            <button type="button" class="btn btn-danger" :disabled="form.processing" @click="deleteUser">
                                <span v-if="form.processing" class="spinner-border spinner-border-sm me-2" />
                                Eliminar cuenta
                            </button>
                        </div>
                    </div>
                </div>
            </div>
            <div class="modal-backdrop fade show" />
        </template>
    </section>
</template>
