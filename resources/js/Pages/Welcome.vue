<script setup>
import { Link } from "@inertiajs/vue3";
import { ref, computed } from "vue";
import { useTheme } from "@/composables/useTheme";

import Start from "../Components/Home/About.vue";
import Footer from "../Components/Footers/Footer.vue";

// Import icons
import lightIcon from "../icons/Logo/icon.png";
import darkIcon from "../icons/Logo/darkicon.png";
import lightmode from "../icons/Mode/sun.png";
import darkmode from "../icons/Mode/moon.png";

const props = defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
    laravelVersion: String,
    phpVersion: String,
});

// Use theme composable
const { isDark, toggleTheme, gradients } = useTheme();

const open = ref(false);

// Computed values for icons
const mode = computed(() => (isDark.value ? darkmode : lightmode));
const iconSrc = computed(() => (isDark.value ? darkIcon : lightIcon));

// Computed gradient text class
const gradientTextClass = computed(() => gradients.text.value);

// Explicit theme toggle handler
const handleThemeToggle = () => {
    toggleTheme();
    // Optional: close mobile menu when toggling theme
    open.value = false;
};

// Mobile menu functions
const closeMenu = () => {
    open.value = false;
};

const handleRouteChange = () => {
    open.value = false;
};
</script>

<template>
    <div class="antialiased">
        <!-- Navbar -->
        <div
            class="relative bg-white dark:bg-neutral-800 shadow-md transition-colors duration-200"
        >
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center h-16">
                    <!-- Logo and Brand -->
                    <div class="flex-shrink-0 flex items-center">
                        <a href="/" class="flex items-center space-x-2">
                            <img class="h-8 w-auto" :src="iconSrc" alt="Icon" />
                            <span
                                :class="[
                                    gradientTextClass,
                                    'text-xl md:text-3xl font-bold tracking-wider bg-clip-text text-transparent transition-all duration-300',
                                ]"
                            >
                                STATSTREAM
                            </span>
                        </a>
                    </div>

                    <!-- Desktop Navigation -->
                    <div
                        v-if="canLogin"
                        class="hidden md:flex items-center space-x-4"
                    >
                        <template v-if="$page.props.auth.user">
                            <Link
                                :href="route('dashboard')"
                                class="text-black dark:text-white hover:bg-neutral-100 dark:hover:bg-neutral-700 px-4 py-2 rounded-lg transition-colors duration-200"
                            >
                                Dashboard
                            </Link>
                        </template>
                        <template v-else>
                            <Link
                                :href="route('login')"
                                class="text-black dark:text-white hover:bg-neutral-100 dark:hover:bg-neutral-700 px-4 py-2 rounded-lg transition-colors duration-200"
                            >
                                Log in
                            </Link>
                            <Link
                                v-if="canRegister"
                                :href="route('register')"
                                class="text-black dark:text-white hover:bg-neutral-100 dark:hover:bg-neutral-700 px-4 py-2 rounded-lg transition-colors duration-200"
                            >
                                Register
                            </Link>
                        </template>
                        <!-- Update the theme toggle button to use handleThemeToggle -->
                        <button
                            @click="handleThemeToggle"
                            class="p-2 rounded-lg bg-stone-900 dark:bg-white hover:bg-stone-700 dark:hover:bg-stone-200 transition-colors duration-200"
                            aria-label="Toggle dark mode"
                        >
                            <img
                                class="h-6 w-6"
                                :src="mode"
                                alt="Theme toggle"
                            />
                        </button>
                    </div>

                    <!-- Mobile menu button -->
                    <div class="md:hidden">
                        <button
                            @click="open = !open"
                            class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-gray-500 dark:hover:text-white hover:bg-gray-100 dark:hover:bg-neutral-700 focus:outline-none transition-colors duration-200"
                            :aria-expanded="open"
                        >
                            <span class="sr-only">Open main menu</span>
                            <svg
                                v-if="!open"
                                class="block h-6 w-6"
                                xmlns="http://www.w3.org/2000/svg"
                                fill="none"
                                viewBox="0 0 24 24"
                                stroke="currentColor"
                            >
                                <path
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    stroke-width="2"
                                    d="M4 6h16M4 12h16M4 18h16"
                                />
                            </svg>
                            <svg
                                v-else
                                class="block h-6 w-6"
                                xmlns="http://www.w3.org/2000/svg"
                                fill="none"
                                viewBox="0 0 24 24"
                                stroke="currentColor"
                            >
                                <path
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    stroke-width="2"
                                    d="M6 18L18 6M6 6l12 12"
                                />
                            </svg>
                        </button>
                    </div>
                </div>
            </div>

            <!-- Mobile menu -->
            <transition
                enter-active-class="transition duration-200 ease-out"
                enter-from-class="transform opacity-0 scale-95"
                enter-to-class="transform opacity-100 scale-100"
                leave-active-class="transition duration-100 ease-in"
                leave-from-class="transform opacity-100 scale-100"
                leave-to-class="transform opacity-0 scale-95"
            >
                <div
                    v-if="open"
                    class="md:hidden absolute w-full bg-white dark:bg-neutral-800 z-50 transition-colors duration-200"
                >
                    <div class="px-2 pt-2 pb-3 space-y-1">
                        <template v-if="$page.props.auth.user">
                            <Link
                                :href="route('dashboard')"
                                class="block px-3 py-2 rounded-md text-base font-medium text-black dark:text-white hover:bg-neutral-100 dark:hover:bg-neutral-700 transition-colors duration-200"
                            >
                                Dashboard
                            </Link>
                        </template>
                        <template v-else>
                            <Link
                                :href="route('login')"
                                class="block px-3 py-2 rounded-md text-base font-medium text-black dark:text-white hover:bg-neutral-100 dark:hover:bg-neutral-700 transition-colors duration-200"
                            >
                                Log in
                            </Link>
                            <Link
                                v-if="canRegister"
                                :href="route('register')"
                                class="block px-3 py-2 rounded-md text-base font-medium text-black dark:text-white hover:bg-neutral-100 dark:hover:bg-neutral-700 transition-colors duration-200"
                            >
                                Register
                            </Link>
                        </template>
                        <button
                            @click="handleThemeToggle"
                            class="w-full text-left px-3 py-2 p-2 rounded-lg bg-stone-900 dark:bg-white text-base font-medium text-black dark:text-white hover:bg-neutral-100 dark:hover:bg-neutral-700 transition-colors duration-200"
                        >
                            <img
                                class="h-6 w-6"
                                :src="mode"
                                alt="Theme toggle"
                            />
                        </button>
                    </div>
                </div>
            </transition>
        </div>

        <Start />
        <Footer />
    </div>
</template>
