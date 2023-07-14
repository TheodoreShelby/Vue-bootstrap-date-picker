<script lang="ts" setup>
const props = defineProps({
  modelValue: {
    type: Number,
    required: true,
  },
  year: {
    type: Number,
    required: true,
  },
  goPreviousMonth: {
    type: Function as PropType<() => void>,
    requried: true,
  },
  goNextMonth: {
    type: Function as PropType<() => void>,
    requried: true,
  },
});

const emits = defineEmits([
  "select-year",
  "previousYear",
  "nextYear",
  "select-month",
]);

const emitSelectedYear = (selectedYear: number) => {
  emits("select-year", selectedYear);
};

const emitSelectedMonth = (event: MouseEvent) => {
  emits("select-month", parseInt(event.target.value));
};

const monthsInYear = [
  "Jan",
  "Feb",
  "Mar",
  "Apr",
  "May",
  "Jun",
  "Jul",
  "Aug",
  "Sep",
  "Oct",
  "Nov",
  "Dec",
];
</script>

<template>
  <div class="month-year">
    <p class="mb-0 d-flex justify-content-between">
      <span class="d-block d-flex">
        <ResetButton
          :icon="'ic:outline-keyboard-arrow-left'"
          @click="goPreviousMonth"
        ></ResetButton>
        <select
          class="form-select pointer pt-0 border-0"
          aria-label="choose month"
          :value="modelValue"
          @click="emitSelectedMonth"
        >
          <option
            v-for="(monthInYear, index) in monthsInYear"
            :key="monthInYear"
            :value="index + 1"
            :selected="index + 1 === modelValue"
          >
            {{ monthInYear }}
          </option>
        </select>
        <ResetButton
          :icon="'ic:outline-keyboard-arrow-right'"
          @click="goNextMonth"
        ></ResetButton>
      </span>
      <span class="d-flex">
        <YearPicker
          @select-year="emitSelectedYear"
          :currentYear="year"
          @previous-year="$emit('previousYear')"
          @next-year="$emit('nextYear')"
        ></YearPicker>
      </span>
    </p>
  </div>
</template>

<style lang="sass" scoped>
@import "~~/assets/sass/color.sass"

$label-height: 24px

.month-year
  height: $label-height
  margin-bottom: 10px

select.form-select
    height: $label-height
    width: 100px
    background-color: transparent
    border-color: transparent
    border-radius: 0
    box-shadow: none

    &:hover
        background-color: $dark-purple

    option
        background-color: $dark-purple
</style>
