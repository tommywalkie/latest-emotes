<template>
  <button
    :class="[
      'px-4 py-2 text-white rounded select-none',
      {
        'bg-gray-400 dark:bg-secondary-300 hover:bg-primary-600 dark:hover:bg-primary-600': !isActive,
        'bg-primary': isActive,
        'opacity-50 cursor-not-allowed': disabled,
      },
      customClass,
    ]"
    :disabled="disabled"
    @click="handleClick"
  >
    <slot />
  </button>
</template>

<script setup lang="ts">
const props = defineProps<{
  isActive?: boolean
  disabled?: boolean
  customClass?: string
}>()

const emit = defineEmits<{
  (e: 'click'): void
}>()

const handleClick = () => {
  if (!props.disabled) {
    emit('click')
  }
}
</script>
