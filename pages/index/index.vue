<template>
  <view class="app-container">
    <view v-for="(component, index) in components" :key="index"></view>
  </view>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
const components = ref([]);
</script>

<style lang="scss">
.app-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between; // 横向排列
  padding: 20rpx;
}
</style>
