<script lang="ts" setup></script>

<template>
  <div
    class="timePicker rounded hideClock d-flex justify-content-center align-items-center"
  >
    ti123me picker
  </div>
</template>

<style lang="sass" scoped>
@import "~~/assets/sass/color.sass"

$picker-size: 300px

.timePicker
  height: $picker-size
  width: 100%
  position: absolute
  background-color: $dark-purple
  top: 105px

.showClock
  animation: showCock .3s ease-in-out forwards

.hideClock
  animation: hideClock .3s ease-in-out forwards


@keyframes showCock
  0%
    transform: translateX($picker-size)
  100%
    transform: translateX(0px)

@keyframes hideClock
  0%
    transform: translateX(0px)

  100%
    transform: translateX($picker-size)
</style>
