<script>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import DeleteUserForm from './Partials/DeleteUserForm.vue';
import UpdatePasswordForm from './Partials/UpdatePasswordForm.vue';
import UpdateProfileInformationForm from './Partials/UpdateProfileInformationForm.vue';
import { Head } from '@inertiajs/vue3';

export default {
    components: {
        AuthenticatedLayout,
        DeleteUserForm,
        UpdatePasswordForm,
        UpdateProfileInformationForm,
        Head,
    },
    props: {
        mustVerifyEmail: {
            type: Boolean,
        },
        status: {
            type: String,
        },
    },
}
</script>

<template>
    <Head title="Perfil" />

    <AuthenticatedLayout>
        <div class="container py-4">
            <div class="row justify-content-center">
                <div class="col-12 col-md-8 col-lg-6">
                    <div class="card shadow-sm mb-4">
                        <div class="card-body">
                            <UpdateProfileInformationForm
                                :must-verify-email="mustVerifyEmail"
                                :status="status"
                            />
                        </div>
                    </div>

                    <div class="card shadow-sm mb-4">
                        <div class="card-body">
                            <UpdatePasswordForm />
                        </div>
                    </div>

                    <div class="card shadow-sm">
                        <div class="card-body">
                            <DeleteUserForm />
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
