<template>
  <div class="dropdown" ref="dropdownRef">
    <a
      href="#"
      class="btn btn-outline-light me-2 dropdown-toggle"
      @click.prevent="toogleOpen"
    >
      {{ title }}
    </a>
    <ul class="dropdown-menu" :style="{ display: 'block' }" v-if="isOpen">
      <slot></slot>
    </ul>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref, onMounted, onUnmounted } from 'vue'
export default defineComponent({
  name: 'Dropdown',
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  setup() {
    const isOpen = ref(false)
    const toogleOpen = () => {
      isOpen.value = !isOpen.value
    }
    // 此处定义的变量名，和上面dom上定义的ref值相同， 并且在setup中要return出去
    // 这样就可以在运行中使用dom对象
    const dropdownRef = ref<HTMLElement | null>(null)
    const handler = (e: MouseEvent) => {
      if (dropdownRef.value) {
        if (
          !dropdownRef.value.contains(e.target as HTMLElement) &&
          isOpen.value
        ) {
          isOpen.value = false
        }
      }
    }
    onMounted(() => {
      document.addEventListener('click', handler)
    })
    onUnmounted(() => {
      document.removeEventListener('click', handler)
    })
    return {
      isOpen,
      toogleOpen,
      dropdownRef,
    }
  },
})
</script>
