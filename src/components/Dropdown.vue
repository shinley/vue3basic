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
import { defineComponent, ref, watch } from 'vue'
import useClickOutside from '@/hooks/useClickOutside'
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
    const dropdownRef = ref<HTMLElement | null>(null)
    const isClickOutside = useClickOutside(dropdownRef)

    watch(isClickOutside, () => {
      if (isOpen.value && isClickOutside) {
        isOpen.value = false
      } else {
        isOpen.value = true
      }
    })

    return {
      isOpen,
      toogleOpen,
      dropdownRef,
    }
  },
})
</script>
