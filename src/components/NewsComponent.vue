<script setup lang="ts">
import {newsType} from "../news.ts";

defineProps<{
  news: newsType;
}>()
</script>

<template>
  <div>
    <h2>{{news.title}}</h2>
    <p>{{news.description}}</p>
    <img :src="news.img_url" alt="news_image">
    <p>{{news.text}}</p>
    <p>{{news.author}}</p>
    <p>{{news.timestamp}}</p>
  </div>
</template>

<style scoped>

</style>