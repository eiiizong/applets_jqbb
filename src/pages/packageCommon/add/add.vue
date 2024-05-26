<template>
  <div class="page-scroll add">
    <ComponentProjectPanel>
      <div class="form">
        <label class="form-item" for="key1">
          <div class="form-item-label">公司名称</div>
          <div class="form-item-input-wrapper">
            <input
              v-model="form.key1"
              class="form-item-input input"
              type="text"
              id="key1"
              placeholder="请输入公司名称"
            />
          </div>
        </label>
        <label class="form-item" for="key2">
          <div class="form-item-label">联系人</div>
          <div class="form-item-input-wrapper">
            <input v-model="form.key2" class="form-item-input input" type="text" id="key2" placeholder="请输入联系人" />
          </div>
        </label>
        <label class="form-item" for="key3">
          <div class="form-item-label">联系电话</div>
          <div class="form-item-input-wrapper">
            <input
              v-model="form.key3"
              class="form-item-input input"
              type="tel"
              id="key3"
              placeholder="请输入联系电话"
            />
          </div>
        </label>
        <label class="form-item" for="key4">
          <div class="form-item-label">项目名称</div>
          <div class="form-item-input-wrapper">
            <input
              v-model="form.key4"
              class="form-item-input input"
              type="text"
              id="key4"
              placeholder="请输入项目名称"
            />
          </div>
        </label>
        <label class="form-item" for="key5">
          <div class="form-item-label">项目地址</div>
          <div class="form-item-input-wrapper">
            <input
              v-model="form.key5"
              class="form-item-input input"
              type="text"
              id="key5"
              placeholder="请输入项目地址"
            />
          </div>
        </label>
        <div class="button-wrapper uno-center">
          <button class="button button-query" @click="onClickQuery">提交</button>
        </div>
      </div>
    </ComponentProjectPanel>
  </div>
</template>

<script setup lang="ts">
  import ComponentProjectPanel from '@/components/project/panel/panel.vue'

  const emit = defineEmits(['query'])

  const form = ref({
    key1: '',
    key2: '',
    key3: '',
    key4: '',
    key5: '',
    key6: ''
  })

  /**
   * 获取筛选条件渲染数据
   */
  const getData = () => {
    //
  }

  const onClickQuery = () => {
    emit('query', form.value)
  }

  onMounted(() => {
    getData()
  })
</script>

<style lang="scss" scoped>
  .add {
    width: 100%;
    padding-top: $spacing;

    .items {
      display: flex;
      flex-direction: column;
    }
    .item {
      margin-bottom: $spacing;
    }
    .button-wrapper {
      width: 100%;

      .button {
        width: 60%;
        height: 80rpx;
        line-height: 80rpx;
        font-size: 28rpx;
        color: #fff;
        text-align: center;
        background-color: $color-primary;
        border-radius: 8rpx;
        margin-right: $spacing;
        box-sizing: border-box;
        font-weight: 500;
      }
    }
  }
</style>
