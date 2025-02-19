<template>
    <AuthenticatedLayout>
        <div class="min-h-screen py-12 px-4 sm:px-6 lg:px-8">
            <!-- Hero Section -->
            <div class="text-center max-w-7xl mx-auto mb-12">
                <h1 class="text-4xl md:text-5xl lg:text-6xl font-extrabold tracking-tight mb-4">
                    <span :class="gradientTextClass">Available Species</span>
                </h1>
                <p class="text-lg text-gray-600 dark:text-gray-300 max-w-2xl mx-auto">
                    Explore our comprehensive collection of timber species and analyze their market trends
                </p>
            </div>

            <!-- Species Grid -->
            <div class="max-w-7xl mx-auto">
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 grid-spacing">
                    <div
                        v-for="item in species"
                        :key="item.speacies"
                        class="group relative"
                    >
                        <Link
                            :href="
                                route('timber-chart.show', {
                                    species: item.speacies,
                                })
                            "
                            class="block h-full"
                        >
                            <div
                                class="relative h-full bg-white dark:bg-neutral-800 rounded-xl shadow-lg dark:shadow-2xl overflow-hidden border border-gray-100 dark:border-neutral-700 p-6 transition-all duration-300 group-hover:shadow-2xl group-hover:-translate-y-1"
                            >
                                <!-- Background Pattern -->
                                <div
                                    class="absolute inset-0 bg-pattern opacity-[0.03] dark:opacity-[0.05]"
                                ></div>

                                <div
                                    class="relative flex flex-col items-center"
                                >
                                    <!-- Icon -->
                                    <div
                                        class="w-16 h-16 mb-4 flex items-center justify-center rounded-lg bg-gradient-to-br from-blue-50 to-teal-50 dark:from-neutral-700 dark:to-neutral-600"
                                    >
                                        <svg
                                            class="w-8 h-8 text-blue-600 dark:text-purple-400"
                                            fill="none"
                                            stroke="currentColor"
                                            viewBox="0 0 24 24"
                                        >
                                            <path
                                                stroke-linecap="round"
                                                stroke-linejoin="round"
                                                stroke-width="2"
                                                d="M12 3c2.755 0 5.455.232 8.083.678.533.09.917.556.917 1.096v1.044a2.25 2.25 0 01-.659 1.591l-5.432 5.432a2.25 2.25 0 00-.659 1.591v2.927a2.25 2.25 0 01-1.244 2.013L9.75 21v-6.568a2.25 2.25 0 00-.659-1.591L3.659 7.409A2.25 2.25 0 013 5.818V4.774c0-.54.384-1.006.917-1.096A48.32 48.32 0 0112 3z"
                                            />
                                        </svg>
                                    </div>

                                    <!-- Species Name -->
                                    <h2
                                        class="text-2xl font-bold text-gray-900 dark:text-white text-center mb-2"
                                    >
                                        {{ item.speacies }}
                                    </h2>

                                    <!-- Decorative line -->
                                    <div
                                        class="mt-4 w-16 h-1 bg-gradient-to-r from-blue-500 to-teal-500 dark:from-purple-500 dark:to-blue-500 rounded-full"
                                    ></div>

                                    <!-- View Details Button -->
                                    <div
                                        class="mt-6 opacity-0 group-hover:opacity-100 transition-opacity"
                                    >
                                        <span
                                            class="inline-flex items-center text-sm font-medium text-blue-600 dark:text-purple-400"
                                        >
                                            View Analysis
                                            <svg
                                                class="w-4 h-4 ml-1 transition-transform group-hover:translate-x-1"
                                                fill="none"
                                                stroke="currentColor"
                                                viewBox="0 0 24 24"
                                            >
                                                <path
                                                    stroke-linecap="round"
                                                    stroke-linejoin="round"
                                                    stroke-width="2"
                                                    d="M9 5l7 7-7 7"
                                                />
                                            </svg>
                                        </span>
                                    </div>
                                </div>

                                <!-- Hover gradient overlay -->
                                <div
                                    class="absolute inset-0 bg-gradient-to-r from-blue-600/0 to-teal-500/0 dark:from-purple-500/0 dark:to-blue-500/0 opacity-0 group-hover:opacity-10 transition-opacity duration-300 rounded-xl"
                                ></div>
                            </div>
                        </Link>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>

<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head } from "@inertiajs/vue3";
import { ref, computed } from "vue";
import { useTheme } from "@/composables/useTheme";

const { isDark, gradients } = useTheme();

// Computed gradient text class
const gradientTextClass = computed(() => gradients.text.value);

const props = defineProps({
    species: Array,
});
</script>
