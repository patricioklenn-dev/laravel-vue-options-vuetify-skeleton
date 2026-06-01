<script>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

export default {
    components: {
        GuestLayout,
        Head,
        Link,
    },
    props: {
        status: {
            type: String,
        },
    },
    data() {
        return {
            form: useForm({}),
        }
    },
    computed: {
        verificationLinkSent() {
            return this.status === 'verification-link-sent';
        },
    },
    methods: {
        submit() {
            this.form.post(route('verification.send'));
        },
    },
}
</script>

<template>
    <GuestLayout>
        <Head title="Email Verification" />

        <div class="card shadow-sm">
            <div class="card-header">Verificación de correo electrónico</div>
            <div class="card-body">
                <p class="text-muted mb-4">
                    Gracias por registrarte! Antes de empezar, podrías verificar tu dirección de correo electrónico haciendo clic en el enlace
                    que te acabamos de enviar? Si no recibiste el correo, te enviaremos otro.
                </p>

                <div v-if="verificationLinkSent" class="alert alert-success mb-4">
                    Un nuevo enlace de verificación ha sido enviado a la dirección de correo electrónico que proporcionaste durante el registro.
                </div>

                <form @submit.prevent="submit">
                    <div class="d-flex justify-content-between align-items-center mt-4">
                        <button type="submit" class="btn btn-primary" :disabled="form.processing">
                            <span v-if="form.processing" class="spinner-border spinner-border-sm me-2" />
                            Reenviar correo de verificación
                        </button>
                        <Link :href="route('logout')" method="post" as="button" class="btn btn-link">Cerrar sesión</Link>
                    </div>
                </form>
            </div>
        </div>
    </GuestLayout>
</template>
