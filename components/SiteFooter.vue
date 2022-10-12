<script setup>
import { ChatIcon } from "@heroicons/vue/solid";
</script>

<template>
    <footer class="site-footer">
        <div class="wrapper flex">
            <div class="copyright">&copy; {{ new Date().getFullYear() }} Geoff Morgenne</div>
            <div class="social-links flex gap-3">
                <NuxtLink to="https://github.com/gmorgenne">
                    GitHub
                </NuxtLink>
                <NuxtLink to="https://www.linkedin.com/in/geoff-morgenne-a323b944">
                    LinkedIn
                </NuxtLink>
                <NuxtLink to="/contact">
                    <ChatIcon class="icon solid" />
                    Contact
                </NuxtLink>
            </div>
        </div>
    </footer>
</template>

<style scoped>
footer {
    @apply p-4 bg-gray-200;
}

.dark-theme footer {
    @apply bg-gray-600;
}

@media screen and (max-width: 768px) {
    footer>.wrapper {
        flex-direction: column-reverse;
    }

    .copyright {
        @apply mt-5;
    }
}

footer>.wrapper {
    @apply flex items-center justify-between max-w-6xl m-auto;
}
</style>