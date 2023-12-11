<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
    <nav
        class="border-2 border-[orange] flex justify-center gap-4 max-w-[1900px] mx-auto py-2"
    >
        <RouterLink class="p-1 border-2 border-black" to="/"
            >Accueil</RouterLink
        >
        <RouterLink class="p-1 border-2 border-black" to="/contact"
            >Contact</RouterLink
        >
        <RouterLink class="p-1 border-2 border-black" to="/api">API</RouterLink>
    </nav>
</template>

<style scoped></style>
