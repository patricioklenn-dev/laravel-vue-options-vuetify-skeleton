<template>
    <div class="min-vh-100 d-flex flex-column">
        <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
            <div class="container-fluid">
                <span class="navbar-brand mb-0 h1">Laravel</span>
                <div class="d-flex gap-2 ms-auto">
                    <button type="button" class="btn btn-link nav-link text-white" @click="$inertia.visit(route('dashboard'))">Panel de control</button>
                    <button type="button" class="btn btn-link nav-link text-white" @click="$inertia.visit(route('profile.edit'))">Perfil</button>
                    <button type="button" class="btn btn-link nav-link text-white" @click="$inertia.post(route('logout'))">Cerrar sesión</button>
                </div>
            </div>
        </nav>
        <main class="flex-grow-1">
            <slot />
        </main>
    </div>
</template>
