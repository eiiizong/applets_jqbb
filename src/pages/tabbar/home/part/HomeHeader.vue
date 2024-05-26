<template>
  <view class="home-header">
    <swiper class="swiper" :current="current" @change="onChange" circular :autoplay="false">
      <swiper-item class="swiper-item swiper-item-01">
        <image class="image" :src="image01"></image>
      </swiper-item>
      <swiper-item class="swiper-item swiper-item-02">
        <image class="image" :src="image02"></image>
      </swiper-item>
      <swiper-item class="swiper-item swiper-item-03">
        <image class="image" :src="image03"></image>
      </swiper-item>
    </swiper>
    <div class="dots">
      <block v-for="(item, index) in 3" :key="index">
        <div class="dot" :class="current === index ? 'active' : ''"></div>
      </block>
    </div>
  </view>
</template>

<script lang="ts" setup>
  import image01 from '../images/01.png'
  import image02 from '../images/02.png'
  import image03 from '../images/03.png'

  const current = ref(0)

  const onChange = (event: WechatMiniprogram.SwiperChange) => {
    const { current: cur } = event.detail
    current.value = cur
  }
</script>

<style lang="scss" scoped>
  .home-header {
    position: relative;
    padding: 0 $spacing;
    .swiper {
      width: 100%;
      height: 306rpx;
      &-item {
        width: 100%;
        position: relative;
      }
      .image {
        width: 100%;
        height: 100%;
      }
    }

    .dots {
      display: flex;
      align-items: center;
      justify-content: center;
      position: absolute;
      left: 50%;
      bottom: 20rpx;
      transform: translateX(-50%);
      .dot {
        width: 10rpx;
        height: 10rpx;
        background-color: #c4c7cc;
        border-radius: 2rpx;
        margin-right: 10rpx;
        transition: width 0.3s ease-in-out;
        &.active {
          width: 20rpx;
          background-image: linear-gradient(135deg, #6ba5fc 0%, #3a86fb 100%);
        }
        &:last-child {
          margin-right: 0;
        }
      }
    }
  }
</style>
