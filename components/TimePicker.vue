<script lang="ts" setup></script>

<template>
  <div
    class="timePicker-container rounded hideClock d-flex justify-content-center align-items-center"
  >
    <div class="timePicker position-relative">
      <div class="time position-absolute">
        <p
          class="d-flex justify-content-center align-items-center"
          style="height: 40px; background-color: red; margin-bottom: 12px"
        >
          <span class="mx-1">
            <input
              type="text"
              style="height: 40px; width: 40px"
              placeholder="07"
              class="text-center"
            />
            <input
              type="text"
              style="height: 40px; width: 40px"
              placeholder="00"
              class="text-center"
            />
          </span>

          <span class="d-flex flex-column mx-2">
            <button style="background-color: blueviolet">AM</button
            ><button style="background-color: blueviolet">PM</button>
          </span>

          <span class="mx-1">
            <button>Select time</button>
          </span>
        </p>
        <div class="clock-container">
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(calc(calc(200px - 25px) / 2), 0)"
            >12</span
          >
          <!-- 11 1 -->
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(43px, -12.5px)"
            >11</span
          >
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(132px, -37.5px)"
            >1</span
          >
          <!-- 10 2 -->
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(10px, -27.5px)"
            >10</span
          >
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(165px, -52.5px)"
            >2</span
          >
          <!-- 9 3 -->
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(0px, -37.5px)"
            >9</span
          >
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(175px, -62.5px)"
            >3</span
          >
          <!-- 8 4 -->
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(11px, -45px)"
            >8</span
          >
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(164px, -70px)"
            >4</span
          >
          <!-- 7 5 -->
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(40px, -64px)"
            >7</span
          >
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(135px, -89px)"
            >5</span
          >
          <!-- 6 -->
          <span
            class="hour d-flex justify-content-center align-items-center"
            style="transform: translate(calc(calc(200px - 25px) / 2), -100px)"
            >6</span
          >
          <span
            class="clock-central d-flex justify-content-center align-items-center"
            style="transform: translate(94px, -202px)"
          ></span>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="sass" scoped>
@import "~~/assets/sass/color.sass"

$picker-size: 300px
$timePicker-container-margin: 24px

.timePicker-container
  height: $picker-size
  width:  $picker-size
  position: absolute
  background-color: $dark-purple
  top: 105px

  .timePicker
    background-color: #ece6f0
    width: 100%
    height: 100%

    .time
      margin: 24px
      width: calc($picker-size - 48px)
      height: calc($picker-size - 48px)

      .clock-container
        background-color: #dfdfdf
        width: 200px
        height: 200px
        margin: 0 auto
        border-radius: 50%

        .hour, .clock-central
          width: 25px
          height: 25px
          padding: 3px
          border-radius: 50%
          transition: .3s
          cursor: pointer

          &:hover
            background-color: $dark-purple
            color: white

        .clock-central
          background-color: $dark-purple
          width: 10px
          height: 10px
          cursor: default

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
