<script setup lang="ts">
import {newsType} from "../news.ts";
import {ref} from "vue";
import jsonObject from "../views-and-likes.json";

const props = defineProps<{
  news: newsType;
}>()

const newsId = props.news.id - 1

const IsVisible = ref(false);
const IsLiked = ref(true);

const views = ref(jsonObject[newsId]["views"]);
const likes = ref(jsonObject[newsId]["likes"]);

function toggleVisible() {
  IsVisible.value = !IsVisible.value;
  if (IsVisible.value) {
    views.value++;
  }
  jsonObject[newsId]["views"] = views.value;
}

function toggleLiked() {
  IsLiked.value = !IsLiked.value;
  if (IsLiked.value) {
    likes.value--;
  } else {
    likes.value++;
  }
  jsonObject[newsId]["views"] = views.value;
}

function addZero() {
  if (props.news.timestamp.getUTCMinutes() < 10) {
    return "0"
  }
  return ""
}

function getDay() {
  switch (props.news.timestamp.getUTCDay()) {
    case 0:
      return "Sonntag"
    case 1:
      return "Montag"
    case 2:
      return "Dienstag"
    case 3:
      return "Mittwoch"
    case 4:
      return "Donnerstag"
    case 5:
      return "Freitag"
    case 6:
      return "Samstag"
  }
  return ""
}

</script>

<template>
  <div id="news-window" @mouseenter="toggleVisible"
       @mouseleave="toggleVisible"
       :style="{ height: IsVisible ? 'auto' : '160px',display: IsVisible ? 'flex' : 'unset' }">
    <h2 id="title">{{ news.title }}</h2>
    <p id="description">{{ news.description }}</p>
    <div id="info" v-if="IsVisible">
      <img :src="news.img_url" alt="news_image">
      <p id="text">{{ news.text }}</p>
    </div>
    <div v-if="IsVisible" id="footer">
      <p>{{
          getDay() + " " + news.timestamp.toLocaleDateString('de-DE') + " " + news.timestamp.getUTCHours() + ":" + news.timestamp.getUTCMinutes() + addZero() + " Uhr"
        }}</p>
      <p id="author">{{ news.author }}</p>
    </div>
    <div v-if="IsVisible" id="view-and-likes">
      <div id="views">
        <img src="\src\auge.png" alt="auge">
        <p>{{ views }}</p>
        <p>&nbsp mal angesehen</p>
      </div>

      <div id="likes">
        <img @click="toggleLiked"
             :src="IsLiked ? '/src/notClickedLikeButton.png' : '/src/ClickedLikeButton.png'"
             alt="like-button"
             id="like-button">
        <p id="like-count">{{ likes }}</p>
      </div>
    </div>


  </div>
</template>

<style scoped>


#news-window {
  height: auto;
  width: 400px;

  border: 2px solid darkslategray;
  border-radius: 50px;

  padding: 30px;
  margin: 50px;

  font-family: sans-serif;

  box-shadow: 5px 5px 5px darkslategray;
  visibility: visible;

  display: flex;
  flex-direction: column;
}

#title {
  font-size: 30px;
  margin: 0;
  padding: 0;
  border-bottom: 3px solid darkslategray;
  border-radius: 2px;
  font-weight: bolder;
  word-break: break-word;
}

#description {
  font-size: 20px;
  margin: 0;
  padding: 0;
  width: 100%;
  text-align: left;
}

#info {
  width: 100%;
  display: flex;
  flex-direction: row;
  margin: 0;
}

#info img {
  width: 200px;
  height: auto
}

#text {
  width: 50%;
  padding-left: 10px;
  text-align: left;
  font-size: 15px;
  line-height: 20px;
}

#footer {
  display: flex;
  flex-direction: column;
  width: 100%;
  text-align: left;
  margin: 0;
  padding: 0;

  font-size: 13px;

}

#view-and-likes {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;

  border-top: 1px solid lightslategray;

}

#views, #likes {
  display: flex;
  flex-direction: row;

  align-items: center;

  font-size: 15px;
}

#views img, #likes img {
  height: 15px;
  width: auto;
  margin-right: 10px;

}


@media screen and (max-width: 550px) {
  #news-window {
    border: 1.897px solid darkslategray;
    padding: 30px;
    margin: 45.69px;
    box-shadow: 4.66px 4.66px 4.66px;
  }

  #title {
    font-size: 28.45px;
    border-bottom: 2px solid darkslategray;
  }

  #description {
    font-size: 19.31px;
  }

  #text {
    padding-left: 9.66px;
    font-size: 14.66px;
    line-height: 19.31px;
  }

  #info img {
    width: 189.66px;
    height: auto
  }

  #footer {
    font-size: 12.34px;
  }

  #view-and-likes {
    border-top: 0.95px solid lightslategray;
  }

  #views, #likes {
    font-size: 14.66px;
  }

  #views img, #likes img {
    height: 14.66px;
    margin-right: 9.66px;
  }
}

@media screen and (max-width: 500px) {
  #news-window {
    border: 1.724px solid darkslategray;
    padding: 29px;
    margin: 42.24px;
    box-shadow: 4.31px 4.31px 4.31px;
  }

  #title {
    font-size: 26.09px;
    border-bottom: 2.61px solid darkslategray;
  }

  #description {
    font-size: 17.24px;
  }

  #text {
    padding-left: 8.62px;
    font-size: 12.93px;
    line-height: 17.24px;
  }

  #info img {
    width: 172.41px;
    height: auto
  }

  #footer {
    font-size: 11.21px;
  }

  #view-and-likes {
    border-top: 1px solid lightslategray;
  }

  #views, #likes {
    font-size: 12.93px;
  }

  #views img, #likes img {
    height: 12.93px;
    margin-right: 8.62px;
  }
}

@media screen and (max-width: 450px) {
  #news-window {
    border: 1.517px solid darkslategray;
    padding: 28px;
    margin: 37.41px;
    box-shadow: 3.79px 3.79px 3.79px;
  }

  #title {
    font-size: 23.48px;
    border-bottom: 2.36px solid darkslategray;
  }

  #description {
    font-size: 15.86px;
  }

  #text {
    padding-left: 7.93px;
    font-size: 11.9px;
    line-height: 15.86px;
  }

  #info img {
    width: 155.17px;
    height: auto
  }

  #footer {
    font-size: 10.34px;
  }

  #view-and-likes {
    border-top: 0.83px solid lightslategray;
  }

  #views, #likes {
    font-size: 11.9px;
  }

  #views img, #likes img {
    height: 11.9px;
    margin-right: 7.93px;
  }
}

@media screen and (max-width: 400px) {
  #news-window {
    border: 1.379px solid darkslategray;
    padding: 27px;
    margin: 33.79px;
    box-shadow: 3.45px 3.45px 3.45px;
  }

  #title {
    font-size: 21.74px;
    border-bottom: 2.17px solid darkslategray;
  }

  #description {
    font-size: 14.62px;
  }

  #text {
    padding-left: 7.31px;
    font-size: 10.97px;
    line-height: 14.62px;
  }

  #info img {
    width: 137.93px;
    height: auto
  }

  #footer {
    font-size: 9px;
  }

  #view-and-likes {
    border-top: 0.76px solid lightslategray;
  }

  #views, #likes {
    font-size: 10.97px;
  }

  #views img, #likes img {
    height: 10.97px;
    margin-right: 7.31px;
  }
}

@media screen and (max-width: 350px) {
  #news-window {
    border: 1.207px solid darkslategray;
    padding: 26px;
    margin: 29.83px;
    box-shadow: 3.02px 3.02px 3.02px;
  }

  #title {
    font-size: 18.97px;
    border-bottom: 1.91px solid darkslategray;
  }

  #description {
    font-size: 12.76px;
  }

  #text {
    padding-left: 6.38px;
    font-size: 9.57px;
    line-height: 12.76px;
  }

  #info img {
    width: 120.69px;
    height: auto
  }

  #footer {
    font-size: 7.93px;
  }

  #view-and-likes {
    border-top: 0.66px solid lightslategray;
  }

  #views, #likes {
    font-size: 9.57px;
  }

  #views img, #likes img {
    height: 9.57px;
    margin-right: 6.38px;
  }
}

@media screen and (max-width: 300px) {
  #news-window {
    border: 1.034px solid darkslategray;
    padding: 25px;
    margin: 25.86px;
    box-shadow: 2.59px 2.59px 2.59px;
  }

  #title {
    font-size: 16.52px;
    border-bottom: 1.66px solid darkslategray;
  }

  #description {
    font-size: 11.03px;
  }

  #text {
    padding-left: 5.52px;
    font-size: 8.28px;
    line-height: 11.03px;
  }

  #info img {
    width: 103.45px;
    height: auto
  }

  #footer {
    font-size: 6.9px;
  }

  #view-and-likes {
    border-top: 0.57px solid lightslategray;
  }

  #views, #likes {
    font-size: 8.28px;
  }

  #views img, #likes img {
    height: 8.28px;
    margin-right: 5.52px;
  }
}

@media screen and (max-width: 250px) {
  #news-window {
    border: 0.862px solid darkslategray;
    padding: 23px;
    margin: 21.55px;
    box-shadow: 2.17px 2.17px 2.17px;
  }

  #title {
    font-size: 13.91px;
    border-bottom: 1.39px solid darkslategray;
  }

  #description {
    font-size: 9.31px;
  }

  #text {
    padding-left: 4.66px;
    font-size: 6.98px;
    line-height: 9.31px;
  }

  #info img {
    width: 86.21px;
    height: auto
  }

  #footer {
    font-size: 5.62px;
  }

  #view-and-likes {
    border-top: 0.48px solid lightslategray;
  }

  #views, #likes {
    font-size: 6.98px;
  }

  #views img, #likes img {
    height: 6.98px;
    margin-right: 4.66px;
  }
}

@media screen and (max-width: 200px) {
  #news-window {
    border: 0.690px solid darkslategray;
    padding: 20px;
    margin: 16.90px;
    box-shadow: 1.72px 1.72px 1.72px;
  }

  #title {
    font-size: 10.43px;
    border-bottom: 1.04px solid darkslategray;
  }

  #description {
    font-size: 6.98px;
  }

  #text {
    padding-left: 3.49px;
    font-size: 5.22px;
    line-height: 6.98px;
  }

  #info img {
    width: 68.97px;
    height: auto
  }

  #footer {
    font-size: 4.48px;
  }

  #view-and-likes {
    border-top: 0.34px solid lightslategray;
  }

  #views, #likes {
    font-size: 5.22px;
  }

  #views img, #likes img {
    height: 5.22px;
    margin-right: 3.49px;
  }
}

@media screen and (max-width: 150px) {
  #news-window {
    border: 0.517px solid darkslategray;
    padding: 17px;
    margin: 12.76px;
    box-shadow: 1.29px 1.29px 1.29px;
  }

  #title {
    font-size: 7.83px;
    border-bottom: 0.79px solid darkslategray;
  }

  #description {
    font-size: 5.24px;
  }

  #text {
    padding-left: 2.62px;
    font-size: 3.93px;
    line-height: 5.24px;
  }

  #info img {
    width: 51.72px;
    height: auto
  }

  #footer {
    font-size: 3.17px;
  }

  #view-and-likes {
    border-top: 0.29px solid lightslategray;
  }

  #views, #likes {
    font-size: 3.93px;
  }

  #views img, #likes img {
    height: 3.93px;
    margin-right: 2.62px;
  }
}

@media screen and (max-width: 100px) {
  #news-window {
    border: 0.345px solid darkslategray;
    padding: 14px;
    margin: 8.62px;
    box-shadow: 0.86px 0.86px 0.86px;
  }

  #title {
    font-size: 5.22px;
    border-bottom: 0.52px solid darkslategray;
  }

  #description {
    font-size: 3.48px;
  }

  #text {
    padding-left: 1.74px;
    font-size: 2.61px;
    line-height: 3.48px;
  }

  #footer {
    font-size: 2.24px;
  }

  #info img {
    width: 34.48px;
    height: auto
  }

  #view-and-likes {
    border-top: 0.29px solid lightslategray;
  }

  #views, #likes {
    font-size: 2.61px;
  }

  #views img, #likes img {
    height: 2.61px;
    margin-right: 1.74px;
  }
}

@media screen and (max-width: 50px) {
  #news-window {
    border: 0.172px solid darkslategray;
    padding: 10px;
    margin: 4.31px;
    box-shadow: 0.43px 0.43px 0.43px;
  }

  #title {
    font-size: 2.61px;
    border-bottom: 0.26px solid darkslategray;
  }

  #description {
    font-size: 1.74px;
  }

  #text {
    padding-left: 0.87px;
    font-size: 1.31px;
    line-height: 1.74px;
  }

  #footer {
    font-size: 1.12px;
  }

  #info img {
    width: 17.24px;
    height: auto
  }

  #view-and-likes {
    border-top: 0.14px solid lightslategray;
  }

  #views, #likes {
    font-size: 1.31px;
  }

  #views img, #likes img {
    height: 1.31px;
    margin-right: 0.87px;
  }
}
</style>