<script setup lang="ts">
import { ref, onMounted, watch } from 'vue'

interface IMenu {
  key: string
  value: string
}
const props = defineProps<{ 
  menuList: Array<IMenu>
  currentValue: string
}>();

let currentValueData = ref(props.currentValue);

onMounted(() => {
  console.log('Menu.vue props', props);
})

const chooseItem = (item: IMenu) => {
  currentValueData.value = item.value;
}

watch(() => props.currentValue, (val) => {
  console.log('currentValueData', val);
  currentValueData.value =  val;
});

</script>

<template>
<div class="cpn-menu">
  <div class="cpn-menu-item" v-for="item in menuList" :key="item.key" @click="chooseItem(item)">
    <span :class="item.value === currentValueData ? 'cpn-menu-item-active' : ''">{{item.value}}</span>
  </div>
</div>
</template>

<style scoped>
.cpn-menu {
  font-size: 28px;
  font-weight: 100;
  display: flex;
  align-items: center;
  padding: 0 20px;
  margin: 20px 0;
}
.cpn-menu-item {
  cursor: pointer;
  margin-right: 20px;
}
.cpn-menu-item-active {
  color: dodgerblue;
}
</style>
