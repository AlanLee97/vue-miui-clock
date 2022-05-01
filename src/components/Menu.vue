<script setup lang="ts">
import { ref, onMounted, watch, defineEmits } from 'vue'

interface IMenu {
  key: string
  value: string
}
const props = defineProps<{ 
  menuList: Array<IMenu>
  currentValue: string
}>();

const emits = defineEmits<{
  (e:string, menu: string, index: number): void
}>();

let currentValueData = ref(props.currentValue);

onMounted(() => {
  console.log('Menu.vue props', props);
})



const chooseItem = (item: IMenu, index: number) => {
  currentValueData.value = item.value;
  emits('menuChange', item.value, index);

}

watch(() => props.currentValue, (val) => {
  console.log('currentValueData', val);
  currentValueData.value = val;
});


</script>

<template>
<div class="cpn-menu">
  <div class="cpn-menu-item" v-for="(item, index) in menuList" :key="item.key" @click="chooseItem(item, index)">
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
