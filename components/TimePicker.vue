<script lang="ts" setup></script>

<template>
  <div
    class="timePicker rounded pullClockDown d-flex justify-content-center align-items-center"
  >
    ti123me picker
  </div>
</template>

<style lang="sass" scoped>
@import "~~/assets/sass/color.sass"

$picker-height: 328px

.timePicker
  height: $picker-height
  width: 100%

  transition: .3s
  background-color: $dark-purple
  transform: translateY(0px)

.pullClockUp
  animation: pullUp .3s ease-in-out forwards

.pullClockDown
  animation: pullDown .3s ease-in-out forwards


@keyframes pullUp
  0%
    transform: translateY(0px)
  100%
    transform: translateY(-361px)

@keyframes pullDown
  0%
    transform: translateY(-361px)
  100%
    transform: translateY(0px)
</style>
