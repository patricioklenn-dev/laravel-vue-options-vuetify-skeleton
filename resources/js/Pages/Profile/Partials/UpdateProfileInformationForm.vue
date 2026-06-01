<script>
import { Link, useForm, usePage } from '@inertiajs/vue3';

export default {
    components: {
        Link,
    },
    props: {
        mustVerifyEmail: {
            type: Boolean,
        },
        status: {
            type: String,
        },
    },
    data() {
        const user = usePage().props.auth.user;
        return {
            user: user,
            form: useForm({
                name: user.name,
                email: user.email,
            }),
        }
    },
}
</script>

<template>
    <section>
        <header class="mb-4">
            <h2 class="h5 mb-2">Información de perfil</h2>
            <p class="text-muted small mb-0">
                Actualiza la información de tu perfil y la direcci?n de correo electr?nico.
            </p>
        </header>

        <form @submit.prevent="form.patch(route('profile.update'))">
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

            <div v-if="mustVerifyEmail && user.email_verified_at === null" class="mt-3">
                <p class="small mb-2">
                    Tu dirección de correo electrónico no esta verificada.
                    <Link
                        :href="route('verification.send')"
                        method="post"
                        as="button"
                        class="btn btn-link p-0 align-baseline"
                    >
                        Haz clic aquí para reenviar el correo de verificación.
                    </Link>
                </p>

                <div
                    v-show="status === 'verification-link-sent'"
                    class="alert alert-success mt-2"
                >
                    Un nuevo enlace de verificación ha sido enviado a tu dirección de correo electrónico.
                </div>
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
