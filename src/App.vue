<script setup lang="ts">

import {newsType, tag} from "./news.ts";
import {news} from "./news.ts";
import {ref} from "vue";
import NewsComponent from "./components/NewsComponent.vue";

const allNews = ref<newsType[]>(news);


const dropdownValue = ref<tag | undefined>(undefined);
const inputValue = ref<string>("");

function filterAndSearch(news: newsType): boolean {
  if (dropdownValue.value == undefined && inputValue.value == ''
      || news.tags.includes(dropdownValue.value) && inputValue.value.toLowerCase() == ''
      || dropdownValue.value == undefined && news.title.toLowerCase().includes(inputValue.value.toLowerCase())
      || news.tags.includes(dropdownValue.value) && news.title.toLowerCase().includes(inputValue.value.toLowerCase())) {
    return true;
  } else {
    return false;
  }
}


</script>

<template>
  <div id="main-parent">
    <div id="main">
      <h1>Neuigkeiten</h1>
      <div id="header">
        <select id="dropdown" v-model="dropdownValue">
          <option :value=undefined>Kein Filter ausgewählt</option>
          <option value="Wirtschaft">Wirtschaft</option>
          <option value="Kriesen">Krisen</option>
          <option value="Technologie">Technologie</option>
          <option value="Politik">Politik</option>
          <option value="Finanzen">Finanzen</option>
          <option value="Sport">Sport</option>
        </select>
        <input id="search" type="text" placeholder="Suche" v-model="inputValue">
      </div>
      <template v-for="(news, index) in allNews">
        <news-component
            v-if="filterAndSearch(news)"
            :key="index" :news="news"/>
      </template>
    </div>
  </div>
</template>

<style scoped>


h1 {
  letter-spacing: 10px;
  font-family: sans-serif;
  font-size: 50px;
  line-height: 2px;
  text-shadow: darkslategray 3px 3px
}

#header {
  background-color: darkslategray;
  width: 100%;
  height: 65px;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  margin: 10px 10px;
  border-radius: 50px;
}

#dropdown {
  margin: auto 17.5px auto 17.5px;
  height: 30px;
  width: 317px;
  padding-left: 10px;
  border-radius: 50px;
  border: 0;
  font-size: 15px
}

#search {
  margin: auto 17.5px auto 17.5px;
  height: 30px;
  width: 300px;
  padding-left: 15px;
  border-radius: 50px;
  border: 0;
  font-size: 15px
}

#main-parent {
  width: 100%;
  display: flex;
  justify-content: center;
}

#main {
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 1750px;
}

@media screen and (max-width: 460px) {
  h1 {
    letter-spacing: 5px;
  }

  #header {
    width: 95%;
    height: 55px;
  }

  #dropdown, #search {
    font-size: 13px;
    height: 25px;
  }
}

@media screen and (max-width: 360px) {
  h1 {
    letter-spacing: 3px;
  }

  #header {
    width: 95%;
    height: 45px;
  }

  #dropdown, #search {
    font-size: 11px;
    height: 20px;
  }
}

@media screen and (max-width: 330px) {
  h1 {
    letter-spacing: 1px;
  }

  #header {
    width: 95%;
    height: 35px;
  }

  #dropdown, #search {
    font-size: 9px;
    height: 15px;
  }
}
</style>
