<template>
  <form class="validate-form-container" action="">
    <slot name="default"></slot>
    <div class="submit-area" @click.prevent="submitForm">
      <slot name="submit">
        <button type="submit" class="btn btn-primary">提交</button>
      </slot>
    </div>
  </form>
</template>
<script lang="ts">
import { defineComponent, onUnmounted } from 'vue'
import mitt from 'mitt'

type Events = {
  formItemCreated: ValidateFunc
}

type ValidateFunc = () => boolean

export const emitter = mitt<Events>()
export default defineComponent({
  emits: ['form-submit'],
  setup(props, context) {
    let funcArr: ValidateFunc[] = []
    const submitForm = () => {
      const result = funcArr.map((func) => func()).every((result) => result)
      context.emit('form-submit', result)
    }

    type callBackFunc = (func: ValidateFunc) => void
    const callback: callBackFunc = (func) => {
      funcArr.push(func)
    }
    // 监听器
    emitter.on('formItemCreated', callback)
    // 卸载时清理监听器
    onUnmounted(() => {
      emitter.off('formItemCreated', callback)
      funcArr = []
    })
    return {
      submitForm,
    }
  },
})
</script>
