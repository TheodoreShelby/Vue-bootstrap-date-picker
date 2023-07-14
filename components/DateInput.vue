<script lang="ts" setup>
const props = defineProps({
  today: {
    type: String as PropType<string>,
  },
});

const emit = defineEmits(["toggleTimepicker"]);

const isDisplayTimeToggler = ref<boolean>(false);
const toggleTime = () => {
  emit("toggleTimepicker");
  isDisplayTimeToggler.value = !isDisplayTimeToggler.value;
};
</script>

<template>
  <p class="date-input d-flex align-items-center position-relative mb-0">
    <input
      class="input rounded w-100"
      type="text"
      placeholder="dd/mm/yyyy"
      :value="today"
      disabled
    />

    <span class="toggleBtns position-absolute rounded-circle d-flex">
      <button
        class="timeToggle toggleBtn rounded-circle p-1 d-flex justify-content-center align-items-center"
        @click="toggleTime"
        :class="isDisplayTimeToggler ? 'displayTimeToggle' : ''"
      >
        <Icon
          name="material-symbols:nest-clock-farsight-analog-outline-rounded"
        />
      </button>

      <button
        class="toggleBtn rounded-circle p-1 d-flex justify-content-center align-items-center"
        @click="$emit('togglePicker')"
      >
        <Icon name="mdi:calendar-blank" />
      </button>
    </span>
  </p>
</template>

<style lang="sass" scoped>
@import "~~/assets/sass/color.sass"

$hoverToggleBackground: #dfdfdf

.input
    font-size: 16px
    border: 2px solid transparent
    outline: none
    background-color: $background-main
    padding: 16px 10px

    &:active
      border: 2px solid transparent

.toggleBtns
  right: calc(24px - 0.25rem)

  .timeToggle
    transform: translateX(36px)
    background-color: $hoverToggleBackground
    opacity: 0

  &:hover
    .timeToggle
      animation: moveRight .3s ease-in-out forwards

  .toggleBtn
    border-color: transparent
    background-color: transparent
    transition: 0.3s

    &:hover
      background-color: $hoverToggleBackground

  .timeToggle.displayTimeToggle
    opacity: 1
    transform: translateX(-10px)

@keyframes moveRight
  0%
    opacity: 0
  100%
    opacity: 1
    transform: translateX(-10px)
</style>
