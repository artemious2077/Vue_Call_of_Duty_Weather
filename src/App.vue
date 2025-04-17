<script setup>
import { ref, onMounted } from 'vue';
import { API_KEY, BASE_URL } from './constants/constants';
import WeatherSummary from './components/WeatherSummary.vue';
import Highlights from './components/Highlights.vue';
import Coordinates from './components/Coordinates.vue';
import Humidity from './components/Humidity.vue';

const city = ref('Moscow');
const weatherInfo = ref(null);

function getWeather() {
  fetch(`${BASE_URL}?q=${city.value}&units=metric&appid=${API_KEY}`)
    .then((res) => res.json())
    .then((data) => weatherInfo.value = data)
}

onMounted(getWeather);
</script>

<template>
  <div class="page">
    <main class="main">
      <div class="container">
        <div class="laptop">
          <div class="tactical-frame tactical-frame--top-left"></div>
          <div class="tactical-frame tactical-frame--top-right"></div>
          <div class="tactical-frame tactical-frame--bottom-left"></div>
          <div class="tactical-frame tactical-frame--bottom-right"></div>
          <div class="sections">
            <section class="section section-left">
              <div class="info">
                <div class="city-inner" @keyup.enter="getWeather">
                  <input v-model="city" type="text" class="search" placeholder="Enter location...">
                  <nav @click="getWeather" class="city-inner__button"></nav>
                </div>
                <WeatherSummary :weatherInfo="weatherInfo" />
              </div>
            </section>
            <section class="section section-right">
              <Highlights :weatherInfo="weatherInfo" />
            </section>
          </div>
          <div class="sections">
            <section class="section-bottom">
              <Coordinates :weatherInfo="weatherInfo" />
            </section>
            <section class="section-bottom">
              <Humidity :weatherInfo="weatherInfo" />
            </section>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<style lang="sass" scoped>
@import './assets/styles/main'

@keyframes glitch
  0%
    transform: translate(0)
  20%
    transform: translate(-2px, 2px)
  40%
    transform: translate(-2px, -2px)
  60%
    transform: translate(2px, 2px)
  80%
    transform: translate(2px, -2px)
  100%
    transform: translate(0)

@keyframes pulse
  0%
    box-shadow: 0 0 0 0 rgba(123, 255, 0, 0.4)
  70%
    box-shadow: 0 0 0 10px rgba(123, 255, 0, 0)
  100%
    box-shadow: 0 0 0 0 rgba(123, 255, 0, 0)

@keyframes tactical-scan
  0%
    opacity: 0
    transform: translateY(-100%)
  50%
    opacity: 0.5
  100%
    opacity: 0
    transform: translateY(100%)

@keyframes radar-ping
  0%
    transform: scale(1)
    opacity: 1
  100%
    transform: scale(1.5)
    opacity: 0

@keyframes flicker
  0%, 100%
    opacity: 1
  50%
    opacity: 0.8

@keyframes border-flash
  0%, 100%
    border-color: #7BFF00
  50%
    border-color: rgba(123, 255, 0, 0.3)

@keyframes border-run
  0%
    background-position: 0% 0%
  100%
    background-position: 200% 0%

.page
  position: relative
  display: flex
  justify-content: center
  align-items: center
  min-height: 100vh
  padding: 100px 0
  background: linear-gradient(to top, #000000, #1a1a1a)
  overflow: hidden
  &::before
    content: ''
    position: absolute
    top: 0
    left: 0
    right: 0
    bottom: 0
    background: url('./assets/img/noise.png')
    opacity: 0.05
    pointer-events: none
  &::after
    content: ''
    position: absolute
    top: 50%
    left: 50%
    width: 200px
    height: 200px
    background: radial-gradient(circle, rgba(123, 255, 0, 0.1) 0%, transparent 70%)
    transform: translate(-50%, -50%)
    animation: radar-ping 2s ease-out infinite
    pointer-events: none

.laptop
  width: 100%
  padding: 20px
  background-color: rgba(14, 16, 15, 0.95)
  border-radius: 4px
  border: 1px solid #7BFF00
  box-shadow: 0 0 20px rgba(123, 255, 0, 0.2)
  backdrop-filter: blur(10px)
  transition: all 0.3s ease
  position: relative
  &::before
    content: ''
    position: absolute
    top: 0
    left: 0
    right: 0
    height: 2px
    background: linear-gradient(90deg, transparent, rgba(123, 255, 0, 0.5), transparent)
    animation: tactical-scan 3s linear infinite
  &:hover
    border-color: rgba(123, 255, 0, 0.8)
    box-shadow: 0 0 30px rgba(123, 255, 0, 0.3)

.sections
  display: flex
  width: 100%
  gap: 20px

  @media (max-width: 767px)
    flex-direction: column

.section-left
  width: 30%
  padding-right: 0

  @media (max-width: 767px)
    width: 100%

.section-right
  width: 70%
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

  @media (max-width: 767px)
    width: 100%
    margin-top: 16px

.city-inner
  position: relative
  display: inline-block
  width: 100%

  &__button
    content: ''
    position: absolute
    top: 0
    right: 10px
    width: 25px
    height: 25px
    background: url('./assets/img/search.svg') no-repeat 50% 50%
    background-size: contain
    transform: translateY(50%)
    cursor: pointer
    filter: invert(88%) sepia(41%) saturate(1485%) hue-rotate(67deg) brightness(119%) contrast(119%)
    transition: all 0.3s ease
    &:hover
      transform: translateY(50%) scale(1.1)
      animation: pulse 1s infinite

.info
  height: 100%
  padding: 16px
  background: rgba(7, 8, 3, 0.8)
  position: relative
  border-radius: 4px
  overflow: hidden
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
    content: '[WEATHER DATA]'
    position: absolute
    top: 5px
    left: 10px
    font-size: 10px
    color: #7BFF00
    opacity: 0.5
    animation: data-fade 2s infinite

.search
  width: 100%
  padding: 16px
  font-family: 'Inter', Arial, sans-serif
  color: #7BFF00
  background-color: rgba(0, 0, 0, 0.75)
  border-radius: 4px
  border: 1px solid rgba(123, 255, 0, 0.3)
  outline: none
  cursor: pointer
  transition: all 0.3s ease
  position: relative
  &::after
    content: '>'
    position: absolute
    right: 40px
    color: #7BFF00
    opacity: 0
    transition: all 0.3s ease
  &:focus
    border-color: #7BFF00
    box-shadow: 0 0 10px rgba(123, 255, 0, 0.2)
    &::after
      opacity: 1
      transform: translateX(10px)
  &::placeholder
    color: rgba(123, 255, 0, 0.5)

.section-bottom
  width: 50%
  margin-top: 16px
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

  @media (max-width: 767px)
    width: 100%

// Tactical UI elements
.tactical-frame
  position: absolute
  pointer-events: none
  transition: all 0.3s ease
  &::after
    content: ''
    position: absolute
    width: 4px
    height: 4px
    background: #7BFF00
    border-radius: 50%
    animation: pulse 2s infinite
  &--top-left
    top: 0
    left: 0
    border-top: 2px solid #7BFF00
    border-left: 2px solid #7BFF00
    width: 20px
    height: 20px
    &::after
      bottom: -2px
      right: -2px
  &--top-right
    top: 0
    right: 0
    border-top: 2px solid #7BFF00
    border-right: 2px solid #7BFF00
    width: 20px
    height: 20px
    &::after
      bottom: -2px
      left: -2px
  &--bottom-left
    bottom: 0
    left: 0
    border-bottom: 2px solid #7BFF00
    border-left: 2px solid #7BFF00
    width: 20px
    height: 20px
    &::after
      top: -2px
      right: -2px
  &--bottom-right
    bottom: 0
    right: 0
    border-bottom: 2px solid #7BFF00
    border-right: 2px solid #7BFF00
    width: 20px
    height: 20px
    &::after
      top: -2px
      left: -2px

.laptop:hover
  .tactical-frame
    &--top-left
      transform: translate(-2px, -2px)
    &--top-right
      transform: translate(2px, -2px)
    &--bottom-left
      transform: translate(-2px, 2px)
    &--bottom-right
      transform: translate(2px, 2px)
</style>
