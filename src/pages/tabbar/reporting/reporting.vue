<template>
  <div class="page reporting">
    <ReportingHeader :tabs="tabs" v-model:value="tab" @query="onClickQuery"></ReportingHeader>

    <scroll-view class="scroll-view" scroll-y>
      <div class="items" v-if="list.length">
        <div class="item" v-for="(item, index) in list" :key="index">
          <ComponentProjectCardProject :render-data="item"></ComponentProjectCardProject>
        </div>
      </div>
      <template v-else>
        <ComponentProjectEmpty v-if="isRequestOver"></ComponentProjectEmpty>
      </template>
    </scroll-view>
  </div>
</template>
<script setup lang="ts">
  import ComponentProjectCardProject from '@/components/project/card-project/card-project.vue'
  import ComponentProjectEmpty from '@/components/project/empty/empty.vue'
  import ReportingHeader from './part/ReportingHeader.vue'

  /**
   * 查询关键词
   */
  const keyord = ref('')
  const tab = ref('1')
  const tabs = [
    {
      key: '1',
      label: '未提交'
    },
    {
      key: '2',
      label: '已提交'
    },
    {
      key: '3',
      label: '已完成'
    }
  ]
  /**
   * 是否查询完成
   */
  const isRequestOver = ref(false)
  /**
   * 查询结果数据
   */
  const list = ref<any[]>([])
  /**
   * 查询数据
   */
  const queryData = () => {
    isRequestOver.value = false
    list.value = [{}, {}, {}]
    // requestAppletGetSubsidyreportingList(chi031.value)
    //   .then((res) => {

    //   })
    //   .finally(() => {
    //     isRequestOver.value = true
    //   })
  }

  /**
   * 点击查询按钮查询
   */
  const onClickQuery = (str: string) => {
    keyord.value = str
    queryData()
  }

  onLoad(() => {
    queryData()
  })
</script>

<style lang="scss" scoped>
  .reporting {
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    .scroll-view {
      flex: 1;
      overflow: hidden;
      .items {
        padding: $spacing;
      }
      .item {
        box-sizing: border-box;
        margin-bottom: $spacing;
        &:last-child {
          margin-bottom: 0;
        }
      }
      .cards {
        .card {
          margin-bottom: $spacing;
          &:last-child {
            margin-bottom: 0;
          }
        }
      }
    }
  }
</style>
