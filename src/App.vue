<!--
 * @Descripttion: 
 * @version: 1.0
 * @Author: xinyan
 * @Date: 2023-09-06 16:05:02
 * @LastEditors: xinyan
 * @LastEditTime: 2024-08-16 15:07:21
-->
<template>
  <div class="content">
    <pro-virtually-list
      :data="list"
      height="400px"
      width="300px"
      :itemCount="10000"
      :itemEstimatedSize="10"
      :buffCount="10"
    >
      <template #slot-scope="{slotProps}">
        <div
          class="li" 
          :style="{
            height: slotProps.data.height + 'px'
          }"
        >
          {{ slotProps.data.text }}
        </div>
      </template>
    </pro-virtually-list>
  </div>
</template>

<script setup>
import ProVirtuallyList from './components/index.vue';
import { ref, onMounted } from 'vue';
component: {
  ProVirtuallyList
}
const value = ref('');
const list = ref([])
onMounted(() => {
  for (let i = 0; i < 10000; i++) {
    list.value.push({text:i + "这是滚动列表的数据！！！", height: Math.max(30, Math.floor(Math.random() * Math.floor(100)))})
  }
})
</script>

<style scoped>
.content {
  background: #fff;
  overflow: hidden;

  .li {
    height: 32px;
    line-height: 32px;
    color: #000;
    font-size: 14px;
  }
}
</style>
