<!-- ./pages/blog/[…slug.vue] -->

<script setup>
const { path } = useRoute();
const { data } = await useAsyncData(`content-${path}`, async () => {
  // fetch document where the document path matches with the cuurent route
  let article = queryContent().where({ _path: path }).findOne();
  // get the surround information,
  // which is an array of documeents that come before and after the current document
  let surround = queryContent()
    .only(["_path", "title", "description"])
    .sort({ date: 1 })
    .findSurround(path);

  return {
    article: await article,
    surround: await surround,
  };
});

// destrucure `prev` and `next` value from data
const [prev, next] = data.value.surround;

// set the meta
useHead({
  title: data.value.article.title,
  meta: [
    { name: "description", content: data.value.article.description },
    {
      hid: "og:image",
      property: "og:image",
      content: `https://site.com/${data.value.article.img}`,
    },
  ],
});
</script>

<template>
  <main id="main" class="article-main">
    <section v-if="data.article" class="article-header">
      <div class="img-cont h-72 mb-12">
        <img
          :src="`/${data.article.img}`"
          :alt="data.article.title"
          class="rounded-2xl"
        />
      </div>
      <h1 class="heading">{{ data.article.title }}</h1>
      <p class="supporting">{{ data.article.description }}</p>
      <h3 class="mt-4">Tags in this article:</h3>
      <ul class="article-tags">
        <li class="tag" v-for="(tag, n) in data.article.tags" :key="n">
          <NuxtLink :to="`/blog/tags/${tag}`">{{ tag }}</NuxtLink>
        </li>
      </ul>
    </section>
    <hr />
    <section class="article-section">
      <aside class="aside">
        <!-- Toc Component -->
        <Toc :links="data.article.body.toc.links" />
      </aside>
      <article class="article">
        <!-- render document coming from query -->
        <ContentRenderer :value="data.article">
          <!-- render rich text from document -->
          <MarkdownRenderer :value="data.article" />

          <!-- display if document content is empty -->
          <template #empty>
            <p>No content found.</p>
          </template>
        </ContentRenderer>
      </article>
    </section>
    <section>
      <h5>View more articles like this one by tag:</h5>
      <ul class="article-tags block">
        <li class="tag" v-for="(tag, n) in data.article.tags" :key="n">
          <NuxtLink :to="`/blog/tags/${tag}`">{{ tag }}</NuxtLink>
        </li>
      </ul>
    </section>
    <!-- PrevNext Component -->
    <PrevNext :prev="prev" :next="next" />
  </main>
</template>

<style scoped>
.article-main {
  @apply p-4 max-w-5xl m-auto;
}

.article-header {
  @apply p-4 pb-12;
}

.article-header .heading {
  @apply font-extrabold text-5xl mb-4;
}

.article-header .supporting {
  @apply font-medium text-lg;
}

.article-section {
  @apply grid grid-cols-8;
}

.aside {
  @apply col-span-full md:col-span-2 row-start-1 w-full pt-14;
}

.aside .toc {
  @apply sticky top-20;
}

.article {
  @apply col-span-full md:col-span-6 md:col-start-1 md:row-start-1 prose w-full p-4 max-w-3xl m-auto;
}

.dark-theme .article {
  @apply prose-invert;
}
</style>
