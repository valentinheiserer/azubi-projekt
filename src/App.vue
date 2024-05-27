<script setup lang="ts">

import {newsType} from "./news.ts";
import {news} from "./news.ts";
import {ref} from "vue";
import NewsComponent from "./components/NewsComponent.vue";

const allNews = ref<newsType[]>(news);

</script>

<template>
<news-component v-for="(news, index) in allNews" :key="index" :news="news"/>
</template>

<style scoped>

</style>
