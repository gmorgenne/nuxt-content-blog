<!-- ./components/Toc.vue -->

<script setup>
// define links prop
defineProps(["links"]);

// flatten TOC links nested arrays to one array
const flattenLinks = (links) => {
  let _links = links
    .map((link) => {
      let _link = [link];
      if (link.children) {
        let flattened = flattenLinks(link.children);
        _link = [link, ...flattened];
      }
      return _link;
    })
    .flat(1);
  return _links;
};
</script>

<template>
  <nav class="toc">
    <div class="toc-header">
      <h3 class="text-xl font-bold">Table of contents</h3>
    </div>
    <ul class="toc-links">
      <!-- render each link with depth class -->
      <li v-for="link of flattenLinks(links)" :key="link.id" :class="`toc-link _${link.depth}`">
        <a :href="`#${link.id}`">
          {{ link.text }}
        </a>
      </li>
    </ul>
  </nav>
</template>

<style scoped>
.toc {
  @apply p-4 bg-slate-100 border border-slate-900 rounded-lg;
  @apply max-h-[calc(100vh-6rem)] overflow-auto;
}

.dark-theme .toc {
  @apply bg-slate-700 border-slate-50;
}

.toc-header {
  @apply pb-2 mb-2 border-b border-slate-400;
}

.toc-links {
  @apply flex flex-col gap-2 px-2;
}

.toc-link {
  @apply text-slate-500;
}

.dark-theme .toc-link {
  @apply text-slate-100;
}

.toc-link._3 {
  @apply pl-3;
}

.toc-link._4 {
  @apply pl-6;
}

.toc-link._undefined {
  @apply pl-8;
}
</style>
