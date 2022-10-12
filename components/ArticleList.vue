<script setup>
const props = defineProps({
    list: Array
})
</script>

<template>
    <ul class="article-list">
        <li v-for="article in list" :key="article._path" class="article-item">
            <NuxtLink :to="article._path">
                <div class="wrapper">
                    <div class="img-cont w-32">
                        <img :src="`/${article.img}`" :alt="article.title" class="rounded-lg max-h-[8rem]" />
                    </div>
                    <div>
                        <h1 class="text-2xl font-semibold">{{ article.title }}</h1>
                        <p>{{ article.description }}</p>
                        <ul class="article-tags">
                            <li class="tag" v-for="(tag, n) in article.tags" :key="n">
                                <NuxtLink :to="`/blog/tags/${tag}`" class="underline">{{ tag }}</NuxtLink>
                            </li>
                        </ul>
                        <p class="text-xs mt-2">{{ article.date }}</p>
                    </div>
                </div>
            </NuxtLink>
        </li>
    </ul>
</template>