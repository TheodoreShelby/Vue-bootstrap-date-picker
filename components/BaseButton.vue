<template>
  <button class="btn-reset px-3 border border-0 text-center">
    <slot></slot>
  </button>
</template>

<style lang="sass" scoped>
@import "~~/assets/sass/color.sass"

.btn-reset
  height: 24px
  outline: none
  background-color: transparent
  transition: 0.5s

.btn-reset:hover
  background-color: $dark-purple
</style>
