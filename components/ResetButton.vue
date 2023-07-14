<script lang="ts" setup>
const props = defineProps({
  icon: {
    type: String as PropType<string>,
  },
});
</script>

<template>
  <button
    class="btn-reset d-flex justify-content-center align-items-center p-0 border border-0 text-center"
  >
    <slot></slot>
    <Icon :name="icon" />
  </button>
</template>

<style lang="sass" scoped>
@import "~~/assets/sass/color.sass"

.btn-reset
  height: 24px
  outline: none
  background-color: transparent
  transition: 0.5s

  &:hover
    background-color: $dark-purple
    color: white
</style>
