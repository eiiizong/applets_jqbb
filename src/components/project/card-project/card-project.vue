<template>
  <div class="card-project">
    <div class="name-wrapper">
      <div class="iconimg iconimg-subsidy"></div>
      <div class="name">{{ renderData?.chi031 || '报备项目名称' }}</div>
    </div>
    <div class="cells">
      <div class="cell">
        <div class="key">产品说明：</div>
        <div class="value">
          {{ renderData?.chm031 || '啊实打实大师撒大大阿达撒撒大声地阿萨大师的阿达阿达阿达阿达是' }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  import type { PropType } from 'vue'
  import type { GetSubsidyProjectListRow } from '@/server/types'

  // import moment from 'moment'
  // import { navigateTo } from '@/utils/uni'

  const props = defineProps({
    /**
     * 渲染内容
     */
    renderData: {
      type: Object as PropType<GetSubsidyProjectListRow>,
      required: false
    }
  })
</script>

<style lang="scss" scoped>
  .card-project {
    width: 100%;
    position: relative;
    padding: 0 $spacing;
    background-color: #fff;
    border-radius: 8rpx;
    box-sizing: border-box;
    .name-wrapper {
      display: flex;
      align-items: center;
      border-bottom: solid 1px rgba($color-primary, 0.1);
      position: relative;
      z-index: 2;
      .iconimg {
        margin-right: 10rpx;
      }
      .name {
        margin: 24rpx 0;
        font-size: 28rpx;
        line-height: 36rpx;
        max-height: 72rpx;
        font-weight: 700;
        color: $color-text;
        @include textOverflow(2);
      }
    }
    .cells {
      position: relative;
      z-index: 2;
      padding: 20rpx 0;
      box-sizing: border-box;
      .cell {
        display: flex;
        line-height: 1.4;
        font-size: 24rpx;
        margin-bottom: 12rpx;
        .key {
          color: rgba($color-text, 0.6);
        }
        .value {
          flex: 1;
          overflow: hidden;
          color: $color-text;
        }
      }
    }
    .button {
      border-top: solid 1px rgba($color-primary, 0.1);
      line-height: 80rpx;
      font-size: 28rpx;
      text-align: center;
      color: $color-primary;
    }
  }
</style>
