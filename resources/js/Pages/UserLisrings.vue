<template>
    <AuthenticatedLayout>
        <h1>HIIII</h1>
        <div
            v-for="listing in listings"
            :key="listing.listings"
            class="bg-black"
        >
            {{ listing.id }}
        </div>
    </AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { defineProps } from "vue";
import { useTheme } from "@/Components/useTheme.js";

const { isDark, toggleTheme } = useTheme();

const props = defineProps({
    listings: {
        type: Array,
        required: true,
    },
});
</script>
