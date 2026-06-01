<script>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';

export default {
    components: {
        AuthenticatedLayout,
        Head,
    },
}
</script>

<template>
    <Head title="Panel de control" />
    <AuthenticatedLayout>
        <div class="container py-4">
            <div class="card shadow-sm">
                <div class="card-header">Panel de control</div>
                <div class="card-body">Estás conectado!</div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
