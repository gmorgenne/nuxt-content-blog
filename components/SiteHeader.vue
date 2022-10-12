<!-- ./components/SiteHeader.vue -->

<template>
  <header class="site-header">
    <div class="wrapper">
      <NuxtLink to="/" class="no-underline">
        <figure class="site-logo flex content-end">
          <img src="/img/LegitStamp.png" alt="logo" class="max-h-8 mr-3" />
          <h1>Geoff Morgenne</h1>
        </figure>
      </NuxtLink>

      <nav class="site-nav flex gap-3">
        <ul class="links flex gap-3">
          <li class="link">
            <NuxtLink to="/about">About</NuxtLink>
          </li>
          <li class="link">
            <NuxtLink to="/blog">Blog</NuxtLink>
          </li>
        </ul>
        <ThemeButton />
      </nav>
    </div>
  </header>
</template>

<style scoped>
.site-header {
  @apply sticky top-0 w-full p-4 bg-red-200 border-b-2 border-white border-opacity-30 backdrop-blur-lg z-20;
}

.dark-theme .site-header {
  @apply bg-red-700;
}

.site-header > .wrapper {
  @apply flex items-center justify-between max-w-6xl m-auto;
}

.site-logo {
  @apply font-black text-lg;
}
</style>
