<!-- ./pages/index.vue -->
<template>
  <main>
    <section class="hero-section">
     <div class="wrapper">
      <h1 class="font-black text-8xl">Welcome to my site</h1>
      <p>Take a look at <NuxtLink to="/blog">my blog</NuxtLink></p>
     </div>
    </section>
  </main>
</template>

<style scoped>
.hero-section {
  @apply flex items-center justify-center text-center w-full h-screen bg-slate-50 text-slate-700;
}

.dark-theme .hero-section {
  @apply bg-slate-700 text-slate-50;
}
</style>