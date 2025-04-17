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

@keyframes scanline
  0%
    transform: translateY(-100%)
  100%
    transform: translateY(100%)

@keyframes data-fade
  0%, 100%
    opacity: 1
  50%
    opacity: 0.7

@keyframes highlight-flash
  0%, 100%
    background: transparent
  50%
    background: rgba(123, 255, 0, 0.1)

@keyframes text-shadow-pulse
  0%, 100%
    text-shadow: 0 0 10px rgba(123, 255, 0, 0.5)
  50%
    text-shadow: 0 0 20px rgba(123, 255, 0, 0.8)

@keyframes tactical-blink
  0%, 100%
    opacity: 1
    transform: scale(1)
  50%
    opacity: 0.5
    transform: scale(0.95)

@keyframes border-run
  0%
    background-position: 0% 0%
  100%
    background-position: 200% 0%

.summary
  position: relative
  transition: all 0.3s ease
  &:hover
    background: rgba(0, 0, 0, 0.6)
    &::before
      opacity: 1
  &::before
    content: ''
    position: absolute
    inset: 0
    border: 1px solid transparent
    border-radius: 4px
    background: linear-gradient(90deg, transparent, #7BFF00, #304C02, #7BFF00, transparent) border-box
    -webkit-mask: linear-gradient(#fff 0 0) padding-box, linear-gradient(#fff 0 0)
    -webkit-mask-composite: destination-out
    mask-composite: exclude
    background-size: 200% 100%
    animation: border-run 4s linear infinite
    opacity: 0.6
    transition: opacity 0.3s ease
  &::after
    content: ''
    position: absolute
    top: 0
    left: 0
    right: 0
    height: 2px
    background: rgba(123, 255, 0, 0.2)
    animation: scanline 4s linear infinite

.pic-main
  width: 60px
  height: 60px
  margin: 20px 0 12px
  background-repeat: no-repeat
  background-position: 50% 50%
  background-size: contain
  filter: brightness(0) invert(88%) sepia(41%) saturate(1485%) hue-rotate(67deg) brightness(119%) contrast(119%)
  opacity: 0.8
  transition: all 0.3s ease
  position: relative
  &::before
    content: ''
    position: absolute
    top: -5px
    left: -5px
    right: -5px
    bottom: -5px
    border: 1px solid rgba(123, 255, 0, 0.3)
    animation: highlight-flash 2s infinite
  &:hover
    transform: scale(1.1)
    opacity: 1

.city
  font-size: 24px
  color: #7BFF00
  text-shadow: 0 0 10px rgba(123, 255, 0, 0.5)
  animation: text-shadow-pulse 2s infinite
  position: relative
  &::after
    content: '[LOCATION]'
    position: absolute
    top: -15px
    right: 0
    font-size: 10px
    opacity: 0.5
    animation: data-fade 2s infinite

.weather
  margin: 0 0 20px
  padding: 20px 0
  border-bottom: 1px solid rgba(123, 255, 0, 0.2)
  position: relative
  transition: all 0.3s ease
  &:hover
    background: rgba(0, 0, 0, 0.4)
    border-bottom-color: transparent
    &::before
      opacity: 1
  &::before
    content: '[CURRENT CONDITIONS]'
    position: absolute
    top: -15px
    left: 0
    font-size: 10px
    color: #7BFF00
    opacity: 0.5
    animation: data-fade 2s infinite

.temp
  padding-bottom: 8px
  font-size: 32px
  color: #7BFF00
  font-family: 'Inter', monospace
  position: relative
  animation: text-shadow-pulse 2s infinite
  &::after
    content: 'TEMPERATURE'
    position: absolute
    top: -10px
    right: 0
    font-size: 10px
    opacity: 0.5
    animation: data-fade 2s infinite

.text-block
  position: relative
  padding-left: 24px
  padding-bottom: 8px
  font-size: 14px
  color: #7BFF00
  transition: all 0.3s ease
  &:hover
    transform: translateX(5px)
    background: rgba(0, 0, 0, 0.4)
    &::after
      opacity: 1
      transform: scaleX(1)
  &::after
    content: ''
    position: absolute
    bottom: 0
    left: 24px
    right: 0
    height: 1px
    background: linear-gradient(90deg, #7BFF00, transparent)
    transform: scaleX(0)
    transform-origin: left
    transition: all 0.3s ease
    opacity: 0

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
    filter: brightness(0) invert(88%) sepia(41%) saturate(1485%) hue-rotate(67deg) brightness(119%) contrast(119%)
    animation: tactical-blink 4s infinite

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