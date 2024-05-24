<script setup lang="ts">
  import { checkAppletAppUpdate } from '@/utils/check'
  import { getSystemInfoSync } from '@/utils/uni'
  import { useCheckLogin } from '@/hooks'
  import { useStoreSystemInfo } from '@/stores/modules'

  onLaunch(() => {
    const systemInfo = getSystemInfoSync()
    const storeSystemInfo = useStoreSystemInfo()

    storeSystemInfo.updateStoreSystemInfo(systemInfo)

    // 小程序检测用户是否登录
    useCheckLogin()
  })
  onShow(() => {
    checkAppletAppUpdate()
  })

  onHide(() => {
    //
  })
</script>

<style lang="scss">
  // 引入全局通用样式
  @use '@/assets/styles/scss/index.scss';
</style>
