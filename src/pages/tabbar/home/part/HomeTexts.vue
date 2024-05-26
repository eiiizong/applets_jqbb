<template>
  <div class="home-con">
    <view class="texts">
      <div class="text">
        这里是产品介绍文字这这里是产品介绍文字这里这里是产品介绍文字这里是产品介绍文字这里这里是产品介绍文字这里是产品介绍文字这里这里是产品介绍文字里这里是产品介绍文字
      </div>

      <div class="btn-wrapper">
        <button class="btn" @click="navigateTo('add', 'packageCommon')">立即报备</button>
      </div>
    </view>
  </div>
</template>

<script lang="ts" setup>
  import { navigateTo } from '@/utils/uni'
</script>

<style lang="scss" scoped>
  .home-con {
    position: relative;
    margin-top: $spacing;
    padding: 0 $spacing;
    box-sizing: border-box;
    .texts {
      background-color: #fff;
      padding: $spacing;
      border-radius: 8rpx;
      box-sizing: border-box;
    }
    .text {
      font-size: 28rpx;
      line-height: 1.4;
      color: rgba($color-text, 0.8);
    }
    .btn-wrapper {
      padding: $spacing 100rpx 0;
      box-sizing: border-box;
    }
    .btn {
      background-color: $color-primary;
      color: #fff;
      font-size: 30rpx;
      line-height: 80rpx;
      border-radius: 50px;
    }
  }
</style>
