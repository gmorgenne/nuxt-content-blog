<!-- ./components/Tags.vue -->

<script setup>
// import icon
import { TagIcon } from "@heroicons/vue/solid";

// tag list state
const expanded = ref(false);

// helper function to flatten tags array
const flatten = (tags, key) => {
  let _tags = tags
    .map((tag) => {
      let _tag = tag;
      if (tag[key]) {
        let flattened = flatten(tag[key]);
        _tag = flattened;
      }
      return _tag;
    })
    .flat(1);
  return _tags;
};

// function to toggle expanded state
const toggleExpand = () => {
  expanded.value = !expanded.value;
};

// get only tags data from `/blog`
const { data } = await useAsyncData("tags", () => queryContent("blog").only(["tags"]).find());

// generate array without duplicates from flattened array
const articleTags = [...new Set(flatten(data.value, "tags"))];
</script>

<template>
  <div class="tag-list" :class="{ active: expanded }">
    <!-- Button to toggle expand -->
    <button @click="toggleExpand" class="cta w-icon">
      <TagIcon class="icon solid" />
      <span>Tags</span>
    </button>
    <ul class="article-tags" :class="{ expanded: expanded }">
      <!-- list out tags with links -->
      <li v-for="(tag, i) in articleTags" :key="i" class="tag">
        <NuxtLink :to="`/blog/tags/${tag}`" class="font-semibold">{{ tag }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<style scoped>
/* ... */
.tag-list {
  @apply flex items-center gap-2 p-2 border border-transparent rounded-lg;
}
.tag-list.active {
  @apply border-slate-200;
}
.article-tags {
  @apply transition-all opacity-0 overflow-hidden duration-200 delay-100 ease-in max-h-0;
}
.article-tags.expanded {
  @apply opacity-100 max-h-full;
}
</style>
