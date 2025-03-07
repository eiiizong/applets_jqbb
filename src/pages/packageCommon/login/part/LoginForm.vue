<template>
  <div class="login-form">
    <div class="button-wrapper">
      <button class="button" :disabled="!isCanClickLogin" open-type="chooseAvatar" @chooseavatar="onChooseAvatar">
        微信一键登录
      </button>
    </div>

    <div class="agreement-wrapper">
      <label for="agree" class="label">
        <checkbox-group @change="onChangeCheckbox">
          <checkbox value="1" id="agree" class="checkbox" />
        </checkbox-group>
        <div class="icon-checkbox" :class="[form.agree ? 'checked' : '']">
          <div class="icon"></div>
        </div>
        <div class="cells" for="agree">
          <div class="cell">
            {{ $t('login.agreement.part01') }}
          </div>
          <div class="cell">
            <span>{{ $t('login.agreement.part02') }}</span>
            <span class="link" @click.stop.prevent="navigateTo('login-user-agreement', 'packageCommon')">
              《{{ $t('login.agreement.part03') }}》
            </span>
            <span>{{ $t('login.agreement.part04') }}</span>
            <span class="link" @click.stop.prevent="navigateTo('login-privacy-policy', 'packageCommon')">
              《{{ $t('login.agreement.part05') }}》
            </span>
          </div>
        </div>
      </label>
    </div>
  </div>
</template>

<script setup lang="ts">
  import type { LoginPageForm } from '@/types'
  import { navigateTo } from '@/utils/uni'

  const emit = defineEmits(['click'])

  /**
   * 登录信息表单
   */
  const form = ref<LoginPageForm>({
    name: '',
    idcard: '',
    tel: '',
    avatar: '',
    agree: false
  })

  /**
   * 是否可以点击登录按钮
   */
  const isCanClickLogin = computed(() => {
    let res = true
    const { agree } = form.value
    if (!agree) {
      res = false
    }

    return res
  })

  /**
   * 用户同意/不同意协议触发的事件
   */
  const onChangeCheckbox = (event: WechatMiniprogram.CheckboxGroupChange) => {
    const { value } = event.detail
    if (value.length) {
      form.value = {
        ...form.value,
        agree: true
      }
    } else {
      form.value = {
        ...form.value,
        agree: false
      }
    }
  }

  /**
   * 图片链接转base64
   */
  const imageUrlTobase64 = (url: string) => {
    return new Promise((resolve, reject) => {
      const fs = uni.getFileSystemManager()
      let suffix = url.substr(url.lastIndexOf('.') + 1)
      let base64 = ''
      try {
        let base64Data = fs.readFileSync(url, 'base64')
        base64 = 'data:image/' + suffix + ';base64,' + base64Data
        resolve(base64)
      } catch (err) {
        reject(err)
      }
    })
  }

  /**
   * 获取头像
   */
  const onChooseAvatar = async (event: any) => {
    const { avatarUrl } = event.detail
    if (avatarUrl) {
      let imgBase64 = ''
      try {
        imgBase64 = (await imageUrlTobase64(avatarUrl)) as string
      } catch (err) {
        //
      }
      form.value.avatar = imgBase64
    }
    emit('click', form.value)
  }
</script>

<style lang="scss" scoped>
  .login-form {
    padding: $spacing;
    box-sizing: border-box;
    padding-top: 150rpx;
    .form-wrapper {
      width: 100%;
      margin-top: $spacing;
      .form-item {
        width: 100%;
        font-size: 28rpx;
        margin-bottom: 26rpx;
        .label {
          font-weight: 500;
          line-height: 32rpx;
          padding-bottom: 8rpx;
          box-sizing: border-box;
          color: rgba($color-text, 0.8);
        }

        .input-wrapper {
          width: 100%;
          display: flex;
          justify-content: space-between;
          width: 100%;
          margin-top: 12rpx;
          height: 80rpx;
          .input {
            flex: 1;
            overflow: hidden;
            background-color: rgba(#f0f2f5, 0.7);
            border-radius: 12rpx;
            line-height: 40rpx;
            height: 100%;
            padding: 20rpx;
            box-sizing: border-box;
            &[disabled] {
              opacity: 0.8;
            }
          }
          .button {
            width: auto;
            padding: 0 20rpx;
            line-height: 80rpx;
            font-size: 28rpx;
            border-radius: 8rpx;
            background-color: $color-primary;
            color: #fff;
            margin-left: $spacing;
            box-sizing: border-box;
          }
        }
      }
    }

    .agreement-wrapper {
      width: 100%;
      margin-top: $spacing;

      .label {
        display: flex;
      }
      .checkbox {
        display: none;
      }
      .icon-checkbox {
        $size: 30rpx;
        width: $size;
        height: $size;
        margin-right: 8rpx;
        border: 1px solid $color-border;
        border-radius: 2px;
        display: flex;
        margin-top: 8rpx;
        box-sizing: border-box;
        .icon {
          margin: auto;
          width: 20rpx;
          height: 10rpx;
          border: 4rpx solid #fff;
          border-radius: 1px;
          border-top: none;
          border-right: none;
          background: transparent;
          transform: rotate(-45deg);
          position: relative;
          top: -2rpx;
          opacity: 0;
          transition: all 0.3s;
          box-sizing: border-box;
        }
        &.checked {
          background-color: $color-primary;
          border: 0;

          .icon {
            opacity: 1;
          }
        }
      }

      .cells {
        flex: 1;
        overflow: hidden;
        .cell {
          color: $color-text-placeholder;
          font-size: 24rpx;
          line-height: 40rpx;
          .link {
            color: $color-primary;
          }
        }
      }
    }
    .button-wrapper {
      padding-top: $spacing * 2;
      box-sizing: border-box;
      .button {
        width: 100%;
        font-size: 30rpx;
        line-height: 80rpx;
        border-radius: 8rpx;
        color: #fff;
        background-color: $color-primary;
        &[disabled] {
          opacity: 0.6;
        }
      }
    }
  }
</style>
