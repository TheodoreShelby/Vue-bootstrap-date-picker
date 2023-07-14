<script lang="ts" setup>
const props = defineProps({
  currentYear: {
    type: Number,
    required: true,
  },
});

const emits = defineEmits(["select-year", "previous-year", "next-year"]);

const isShowYearPicker = ref<boolean>(false);

const toggleYearPicker = () => {
  isShowYearPicker.value = !isShowYearPicker.value;
};

const selectYear = (selectedYear: number) => {
  emits("select-year", selectedYear);
  toggleYearPicker();
};

const startYear = ref<number>(props.currentYear - (props.currentYear % 10));

const yearsToRender = ref<number[]>([]);

const addYears = () => {
  for (let y = startYear.value; y <= startYear.value + 15; y++) {
    yearsToRender.value.push(y);
  }
};
addYears();

const setStartYear = (year: number) => {
  startYear.value += year;
  addYears();
};

const renderYears = () => {
  if (yearsToRender.value.includes(props.currentYear)) return;

  if (props.currentYear < startYear.value) {
    yearsToRender.value = [];
    setStartYear(-15);
  } else if (props.currentYear > startYear.value + 15) {
    yearsToRender.value = [];
    setStartYear(15);
  }
};

watch(
  () => props.currentYear,
  () => renderYears()
);
</script>

<template>
  <ResetButton
    :icon="'ic:outline-keyboard-arrow-left'"
    @click="$emit('previous-year')"
  ></ResetButton>
  <div class="year-picker position-relative">
    <ResetButton :icon="'ic:round-arrow-drop-down'" @click="toggleYearPicker">
      <template #default>
        <span>{{ currentYear }}</span>
      </template>
    </ResetButton>
    <div
      class="year-container p-1 position-absolute justify-content-center align-items-center"
      :class="`${isShowYearPicker ? 'show' : 'hide'}`"
    >
      <div class="years">
        <div
          class="year d-flex justify-content-center align-items-center pointer"
          v-for="year in yearsToRender"
          :key="year"
          :class="{ currentYear: year === currentYear }"
          @click="selectYear(year)"
        >
          {{ year }}
        </div>
      </div>
    </div>
  </div>
  <ResetButton
    :icon="'ic:outline-keyboard-arrow-right'"
    @click="$emit('next-year')"
  ></ResetButton>
</template>

<style lang="sass" scoped>
@import "~~/assets/sass/color.sass"

$grid-size: 280px
$grid-gap: 10px
$cell-size: 300px

.year-container
  width: $cell-size
  margin-left: -206px
  height: $cell-size
  background-color: $background-main

  .years
    width: $grid-size
    height: $grid-size
    display: grid
    grid-template-columns: repeat(4,1fr)
    grid-template-rows: repeat(4,  calc(($grid-size - ($grid-gap * 3)) / 4))
    gap: $grid-gap

    .year
      border: 1px solid transparent
      border-radius: 8px

      &:hover
        border-color: $dark-purple

    .year.currentYear
      background-color: $dark-purple !important
      color: white

.year-container.hide
  margin-left: 306px

.show
    animation: openYearPicker .5s ease-in

.hide
    animation: closeYearPicker .5s ease-in

@keyframes openYearPicker
  0%
    width: 0px
    margin-left: 306px
  100%
    width: $grid-size

@keyframes closeYearPicker
  0%
    width: $grid-size
    margin-left: -206px
  100%
    width: 0px
    margin-left: 306px
</style>
