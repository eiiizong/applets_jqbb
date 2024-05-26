<template>
  <div class="project-header">
    <div class="search-wrapper">
      <input
        v-model="keyword"
        class="input"
        type="text"
        confirm-type="search"
        placeholder-style="color:rgba(255, 255, 255, 0.8);"
        :placeholder="$t('project.header.searchPlaceholder')"
        @confirm="onSearch"
      />
    </div>

    <div class="tabs">
      <div
        class="tab"
        v-for="item in tabs"
        :key="item.key"
        :class="[item.key === value ? 'checked' : '']"
        @click="onClick(item.key)"
      >
        <div class="text">{{ item.label }}</div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
  import type { PropType } from 'vue'

  const emit = defineEmits(['query', 'update:value'])

  const props = defineProps({
    /**
     * 渲染数据
     */
    tabs: {
      type: Array as PropType<
        {
          key: string
          label: string
        }[]
      >,
      required: true
    },
    /**
     * 当前滚动到顶部的id
     */
    value: {
      type: String,
      required: true
    }
  })

  /**
   * 查询关键词
   */
  const keyword = ref('')

  /**
   * 点击查询按钮
   */
  const onSearch = () => {
    emit('query', keyword.value)
  }

  const onClick = (key: string) => {
    if (props.value !== key) {
      emit('update:value', key)
    }
  }
</script>

<style lang="scss" scoped>
  $scroll-view-height: 96rpx;
  .project-header {
    width: 100%;
    background-color: $color-primary;

    .search-wrapper {
      padding: $spacing;
      box-sizing: border-box;
      .input {
        display: block;
        width: 100%;
        height: 72rpx;
        border-radius: 50px;
        background-color: rgba(#ffff, 0.6);
        padding: 16rpx 24rpx;
        font-size: 28rpx;
        line-height: 40rpx;
        font-weight: 400;
        text-align: left;
        color: #fff;
        box-sizing: border-box;
      }
    }

    .tabs {
      width: 100%;
      height: $scroll-view-height;
      white-space: nowrap;
      overflow: hidden;
      background-color: #fff;
      border-bottom: 1px solid $color-border;
      .tab {
        width: 33.33%;
        display: inline-block;
        padding-left: $spacing;
        box-sizing: border-box;
        .text {
          line-height: $scroll-view-height;
          font-size: 32rpx;
          color: $color-text;
          position: relative;
          transition: all 0.3s;
          text-align: center;
          &::before {
            content: '';
            width: 0;
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            bottom: 0;
            height: 0;
            border-radius: 50px;
            transition: all 0.3s;
          }
        }

        &:last-child {
          padding-right: $spacing;
        }
        &.checked {
          color: $color-primary;
          font-weight: 700;
          .text {
            &::before {
              width: 80%;
              height: 6rpx;
              background-color: $color-primary;
            }
          }
        }
      }
    }
  }
</style>
