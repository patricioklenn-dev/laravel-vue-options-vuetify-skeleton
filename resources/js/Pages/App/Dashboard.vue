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
        <v-container>
            <v-card>
                <v-card-title>Panel de control</v-card-title>
                <v-card-text>Estás conectado!</v-card-text>
            </v-card>
        </v-container>
    </AuthenticatedLayout>
</template>
