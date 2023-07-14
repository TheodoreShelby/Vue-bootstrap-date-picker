<template>
  <div class="weekdays text-center">
    <div
      class="weekday"
      v-for="weekday in ['Su', 'Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa']"
      :key="weekday"
    >
      {{ weekday }}
    </div>
  </div>
</template>

<style lang="sass" setup>
.weekdays
  height: 24px
  margin-bottom: 6px
  display: grid
  grid-template-columns: repeat(7, 1fr)
</style>
