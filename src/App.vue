<script setup>
import { RouterLink, RouterView } from "vue-router";
import NavigationComponent from "./components/NavigationComponent.vue";
</script>

<template>
    <header>
        <NavigationComponent></NavigationComponent>
    </header>

    <main class="max-w-[1900px] mx-auto p-2">
        <RouterView />
    </main>
</template>

<style scoped></style>
