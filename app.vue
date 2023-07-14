<script lang="ts" setup>
import "bootstrap/dist/js/bootstrap.js";

const time = new Date();
const date = ref<number>(time.getDate());
const month = ref<number>(time.getMonth() + 1);
const year = ref<number>(time.getFullYear());

const formatData = (value: number) => {
  return value < 10 ? `0${value}` : value.toString();
};

const today = computed(() => {
  return `${formatData(date.value)} / ${formatData(month.value)} / ${
    year.value
  } HH:MM`;
});

const togglePicker = () => {
  const datePickerElement = document.getElementsByClassName("date-picker")[0];
  datePickerElement.classList.toggle("scrolldown");
  datePickerElement.classList.toggle("scrollup");

  const timePickerElement = document.getElementsByClassName("timePicker")[0];
  if (timePickerElement.classList.contains("showClock")) {
    timePickerElement.classList.toggle("showClock");
    timePickerElement.classList.toggle("hideClock");
  }
};

const goPreviousMonth = () => {
  month.value--;
  if (month.value < 1) {
    month.value = 12;
    goPreviousYear();
  }
};

const goNextMonth = () => {
  month.value++;
  if (month.value > 12) {
    month.value = 1;
    nextYear();
  }
};

const goPreviousYear = () => {
  year.value--;
  if (year.value === 0) return;
};

const nextYear = () => {
  year.value++;
};

const selectDay = (day: number | null) => {
  if (!day) return;
  date.value = day;
};

const getDaysCount = (yyyy: number, mm: number) => {
  return new Date(yyyy, mm, 0).getDate();
};

const daysCount = computed(() => {
  return getDaysCount(year.value, month.value);
});

const renderDates = () => {
  const firstWeekdayInMonth = new Date(
    `${year.value}-${month.value}-1`
  ).getDay();

  const daysCountOfLastMonth = getDaysCount(year.value, month.value - 1);

  const daysOfLastMonth = daysCountOfLastMonth - firstWeekdayInMonth + 1;
  const daysToRender: Array<number | null> = new Array(
    daysCountOfLastMonth - daysOfLastMonth + 1
  ).fill(null);

  for (let i = 1; i <= daysCount.value; i++) {
    daysToRender.push(i);
  }

  return daysToRender;
};

const selectYear = (yyyy: number) => {
  year.value = yyyy;
};

const selectedMonth = (mm: number) => {
  month.value = mm;
};

const toggleTimePicker = () => {
  const timePickerElement = document.getElementsByClassName("timePicker")[0];
  timePickerElement.classList.toggle("showClock");
  timePickerElement.classList.toggle("hideClock");

  const datePickerElement = document.getElementsByClassName("date-picker")[0];
  if (datePickerElement.classList.contains("scrollup")) {
    datePickerElement.classList.toggle("scrolldown");
    datePickerElement.classList.toggle("scrollup");
  }
};
</script>

<template>
  <div class="container d-flex justify-content-center">
    <div class="date-picker mt-5 scrollup rounded overflow-hidden">
      <DateInput
        :today="today"
        @togglePicker="togglePicker"
        @toggleTimepicker="toggleTimePicker"
      ></DateInput>
      <hr style="width: 90%; margin: 0 auto" />
      <div class="picker rounded">
        <MonthYearPicker
          :modelValue="month"
          :year="year"
          :goPreviousMonth="goPreviousMonth"
          :goNextMonth="goNextMonth"
          @select-year="selectYear"
          @previous-year="goPreviousYear"
          @next-year="nextYear"
          @select-month="selectedMonth"
        ></MonthYearPicker>
        <WeekDaysTitle></WeekDaysTitle>
        <div class="dates">
          <div
            class="date d-flex justify-content-center align-items-center pointer rounded-circle"
            v-for="(day, index) in renderDates()"
            :key="index"
            :class="{ currentDate: day === date, disable: day === null }"
            @click="selectDay(day)"
            :style="{ cursor: day ? 'pointer' : 'default' }"
          >
            {{ day }}
          </div>
        </div>

        <div class="confirm-select d-flex justify-content-end">
          <BaseButton @click="togglePicker">OK</BaseButton>
        </div>
      </div>

      <TimePicker></TimePicker>
    </div>
  </div>
</template>

<style lang="sass" scoped>
@import "~~/assets/sass/color.sass"

$row-height: 40px
$row-count: 6
$dates-height: calc($row-height * $row-count)
$default-height: 60px
$picker-height: 328px
$label-height: 24px
$date-picker-mt: 20px
$date-picker-mb: 12px
$date-picker-border-width: 2px
$scrolldown-height: calc($default-height + $picker-height + $date-picker-mt + $date-picker-mb + $date-picker-border-width + 2px)

.date-picker
  width: 304px
  height: $default-height
  border: $date-picker-border-width solid $background-main
  background-color: $background-main
  position: relative

.date-picker:hover,
.date-picker.scrolldown
  border-color: $dark-purple

.scrolldown
  animation: scrolldown 0.3s ease-in-out forwards

@keyframes scrolldown
  0%
    height: $default-height
  100%
    height: $scrolldown-height

.scrollup
  animation: scrollup 0.5s forwards

@keyframes scrollup
  0%
    height: $scrolldown-height
  100%
    height: $default-height

.picker
  margin: $date-picker-mt 12px $date-picker-mb
  height: $picker-height

  /* date picking area */
  .dates
    height: $dates-height
    display: grid
    grid-template-columns: repeat(7, 1fr)
    grid-template-rows: repeat($row-count, $row-height)

    .date
      transition: .1s
      border: 1px solid transparent

      &:hover
        border-color:  $dark-purple

    .date.disable
      &:hover
        border-color: transparent

  .currentDate
    background-color: $dark-purple
    color: white

    &:hover
      background-color: $dark-purple !important

  /* confirm */
  .confirm-select
    height: $label-height
    button
      &:hover
        color: white
</style>
