<script setup>
import { capitalizeFirstLetter, today } from '../utils/utils'

const props = defineProps({
  weatherInfo: {
    required: true,
    type: [Object, null],
  }
})

</script>

<template>
  <main v-if="weatherInfo?.weather" class="summary">
    <article :style="`background-image: url('./src/assets/img/weather-main/${weatherInfo?.weather[0].description}.png');`"
      class="pic-main">
    </article>
    <section class="weather">
      <div class="temp">
        {{ Math.round(weatherInfo?.main.temp) }} °C
      </div>
      <div class="weather-desc text-block">
        {{ capitalizeFirstLetter(weatherInfo?.weather[0].description) }}
      </div>
    </section>
    <article class="city text-block">
      {{ weatherInfo?.name }},
      {{ weatherInfo?.sys.country }}
    </article>
    <article class="date text-block">
      {{ today }}
    </article>
  </main>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'
.pic-main
  width: 60px
  height: 60px
  margin: 20px 0 12px
  background-repeat: no-repeat
  background-position: 50% 50%
  background-size: contain

.city
  font-size: 24px

.weather
  margin: 0 0 20px
  padding: 20px 0
  border-bottom: 1px solid rgba(255, 255, 255, 0.4)

.temp
  padding-bottom: 8px
  font-size: 32px

.text-block
  position: relative
  padding-left: 24px
  padding-bottom: 8px
  font-size: 14px

  &::before
    content: ''
    position: absolute
    top: 0
    left: 0
    width: 20px
    height: 20px
    margin-right: 6px
    background-repeat: no-repeat
    background-position: 50% 50%
    background-size: contain

.weather-desc

  &::before
    background-image: url('/src/assets/img/weather.svg')

.city

  &::before
    background-image: url('/src/assets/img/location.svg')

.date

  &::before
    left: 2px
    width: 15px
    height: 15px
    background-image: url('/src/assets/img/calendar.svg')
</style>