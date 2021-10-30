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
  formItemCreated: string
}

export const emitter = mitt<Events>()
export default defineComponent({
  emits: ['form-submit'],
  setup(props, context) {
    const submitForm = () => {
      context.emit('form-submit', true)
    }

    type callBackFunc = (data: string) => void
    const callback: callBackFunc = (test) => {
      console.log(test)
    }
    // 监听器
    emitter.on('formItemCreated', callback)
    // 卸载时清理监听器
    onUnmounted(() => {
      emitter.off('formItemCreated', callback)
    })
    return {
      submitForm,
    }
  },
})
</script>
