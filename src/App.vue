<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import {ref} from 'vue';
import Menu from './components/Menu.vue';
import SettingBar from './components/SettingBar.vue';
import { NCarousel } from 'naive-ui'

const menuList = [
  {
    key: 'alarm',
    value: '闹钟',
    img: 'https://naive-ui.oss-cn-beijing.aliyuncs.com/carousel-img/carousel1.jpeg',
  },
  {
    key: 'time',
    value: '时钟',
    img: 'https://naive-ui.oss-cn-beijing.aliyuncs.com/carousel-img/carousel2.jpeg',
  },
  {
    key: 'second',
    value: '秒表',
    img: 'https://naive-ui.oss-cn-beijing.aliyuncs.com/carousel-img/carousel3.jpeg',

  },
  {
    key: 'counter',
    value: '计时',
    img: 'https://naive-ui.oss-cn-beijing.aliyuncs.com/carousel-img/carousel4.jpeg',

  },
];

let carouselIndex = ref(0);

const carouselIndexChange = (index: number) => {
  console.log('当前页', index);
  carouselIndex.value = index;
  
}

const menuChange = (menu: string, index: number = 0) => {
  console.log('app.vue menu', menu);
  currentIndex.value = index;
  
}

let currentIndex = ref(0);
</script>

<template>
<div class="app">
  <SettingBar />
  <Menu :menuList="menuList" :currentValue="menuList[carouselIndex]['value']" @menuChange="menuChange" />
  <div class="swiper-item-container">
    <n-carousel :current-index="currentIndex" :show-dots="false" @update:current-index="carouselIndexChange">
      <div class="swiper-item" v-for="item in menuList" :key="item.img">
        <img
          class="carousel-img"
          :src="item.img"
        >
      </div>
    </n-carousel>
  </div>
</div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  height: 100vh;
  overflow: scroll;
}

.swiper-item-container {
  flex: 1;
  border: 1px solid red;
}

.swiper-item {
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}

.carousel-img {
  width: 100%;
  height: 240px;
  object-fit: cover;
}
</style>
