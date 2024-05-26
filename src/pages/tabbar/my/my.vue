<template>
  <div class="page-scroll my">
    <div class="my-header">
      <div class="avatar-wrapper uno-center uno-flex-col">
        <image class="image" :src="imageAvatar" @click="onClickLogin"></image>
        <div class="name" @click="onClickLogin">{{ token ? name : '立即登录' }}</div>
      </div>
    </div>
    <div class="nav-wrapper">
      <div class="nav-item uno-flex uno-items-center uno-justify-between">
        <div class="key">手机号</div>
        <div class="value">
          <div class="text">13200000000</div>
        </div>
      </div>
      <div class="nav-item uno-flex uno-items-center uno-justify-between" @click="switchTab('reporting')">
        <div class="key">我的报备</div>
        <div class="value uno-flex uno-items-center">
          <div class="text"></div>
          <ta-icon name="arrow" size="28rpx"></ta-icon>
        </div>
      </div>
      <div class="nav-item uno-flex uno-items-center uno-justify-between">
        <div class="key">关于</div>
        <div class="value uno-flex uno-items-center">
          <div class="text">了解更多</div>
          <ta-icon name="arrow" size="28rpx"></ta-icon>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  import imageAvatar from './images/avatar.png'
  import { switchTab, navigateTo } from '@/utils/uni'

  import { useStoreUserInfo } from '@/stores/modules'

  const storeUserInfo = useStoreUserInfo()

  const { name, token } = toRefs(storeUserInfo)

  const onClickLogin = () => {
    if (token?.value) {
      return
    }
    navigateTo('login', 'packageCommon')
  }
</script>

<style lang="scss" scoped>
  .my {
    width: 100%;
    position: relative;
    &-header {
      width: 100%;
      height: 300rpx;
      background-image: linear-gradient(to bottom, $color-primary, rgba($color-primary, 0.2));
      color: #fff;
      padding-top: $spacing;
      box-sizing: border-box;

      .image {
        width: 120rpx;
        height: 120rpx;
        border-radius: 50%;
      }
      .name {
        font-size: 28rpx;
        line-height: 40rpx;
      }
    }
    .nav-wrapper {
      width: 750rpx - $spacing * 2;
      position: absolute;
      top: 250rpx;
      left: 50%;
      transform: translateX(-50%);
      background-color: #fff;
      border-radius: 32rpx;
      padding: $spacing;
      box-sizing: border-box;
      .nav-item {
        line-height: 80rpx;
        font-size: 30rpx;
        .key {
          font-weight: 500;
        }
        .value {
          color: rgba($color-text, 0.4);
          font-size: 28rpx;
        }
        .text {
          color: $color-primary;
        }
      }
    }
  }
</style>
