<script setup>
import { getPresure, sun } from "../utils/utils";
import VanillaTilt from 'vanilla-tilt';
import { onMounted } from 'vue';

const props = defineProps({
  weatherInfo: {
    required: true,
    type: [Object, null],
  },
});

onMounted(() => {
  VanillaTilt.init(document.querySelectorAll(".card"), {
    max: 10,
    speed: 400,
    scale: 1.05,
    glare: true,
    "max-glare": 0.2,
    gyroscope: true
  });
});
</script>

<template>
  <main class="section highlights">
    <div class="title">Today's Highlights</div>
    <div class="highlights-wrapper">
      <div class="highlights-grid">
        <!-- Wind -->
        <section class="card" data-tilt data-tilt-max="10" data-tilt-scale="1.05">
          <div class="card-tooltip">
            <img src="../assets/img/wind.webp" alt="Wind tactical" class="tooltip-image">
            <div class="tooltip-content">
              <h3>TACTICAL ADVICE: WIND</h3>
              <p>Strong winds detected. Adjust movement patterns. Stay in cover and avoid open areas. Wind affects ballistics.</p>
            </div>
          </div>
          <div class="card-header">
            <div class="card-title">Wind</div>
            <div class="card-icon">
              <svg viewBox="0 0 24 24" class="tactical-icon">
                <path d="M12,16A3,3 0 0,1 9,13C9,11.88 9.61,10.9 10.5,10.39L20.21,4.77L14.68,14.35C14.18,15.33 13.17,16 12,16M12,3C13.81,3 15.5,3.5 16.97,4.32L14.87,5.53C14,5.19 13,5 12,5A8,8 0 0,0 4,13C4,15.21 4.89,17.21 6.34,18.65H6.35C6.74,19.04 6.74,19.67 6.35,20.06C5.96,20.45 5.32,20.45 4.93,20.07V20.07C3.12,18.26 2,15.76 2,13A10,10 0 0,1 12,3M22,13C22,15.76 20.88,18.26 19.07,20.07V20.07C18.68,20.45 18.05,20.45 17.66,20.06C17.27,19.67 17.27,19.04 17.66,18.65V18.65C19.11,17.2 20,15.21 20,13C20,12 19.81,11 19.46,10.1L20.67,8C21.5,9.5 22,11.18 22,13Z" />
              </svg>
            </div>
          </div>
          <div class="card-content">
            <div class="value-group">
              <div class="value">{{ weatherInfo?.wind.speed }}<span class="unit">m/s</span></div>
              <div class="value">{{ weatherInfo?.wind.deg }}<span class="unit">deg</span></div>
            </div>
          </div>
        </section>

        <!-- Pressure -->
        <section class="card" data-tilt data-tilt-max="10" data-tilt-scale="1.05">
          <div class="card-tooltip">
            <img src="../assets/img/compass.png" alt="Pressure tactical" class="tooltip-image">
            <div class="tooltip-content">
              <h3>TACTICAL ADVICE: PRESSURE</h3>
              <p>High pressure system. Enhanced visibility. Optimal conditions for long-range engagement.</p>
            </div>
          </div>
          <div class="card-header">
            <div class="card-title">Pressure</div>
            <div class="card-icon">
              <svg viewBox="0 0 24 24" class="tactical-icon">
                <path d="M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2M12,4A8,8 0 0,1 20,12C20,14.4 19,16.5 17.3,18C15.9,16.7 14,16 12,16C10,16 8.2,16.7 6.7,18C5,16.5 4,14.4 4,12A8,8 0 0,1 12,4M14,6H10V8H14V6M12,9A4,4 0 0,0 8,13A4,4 0 0,0 12,17A4,4 0 0,0 16,13A4,4 0 0,0 12,9Z" />
              </svg>
            </div>
          </div>
          <div class="card-content">
            <div class="value-group">
              <div class="value">{{ getPresure(weatherInfo?.main.pressure) }}<span class="unit">mm</span></div>
            </div>
          </div>
        </section>

        <!-- Feels Like -->
        <section class="card" data-tilt data-tilt-max="10" data-tilt-scale="1.05">
          <div class="card-tooltip">
            <img src="../assets/img/bg-warm.jpg" alt="Temperature tactical" class="tooltip-image">
            <div class="tooltip-content">
              <h3>TACTICAL ADVICE: TEMP</h3>
              <p>Temperature affects stamina. Maintain hydration. Watch for heat signatures in thermal vision.</p>
            </div>
          </div>
          <div class="card-header">
            <div class="card-title">Feels Like</div>
            <div class="card-icon">
              <svg viewBox="0 0 24 24" class="tactical-icon">
                <path d="M15 13V5A3 3 0 0 0 9 5V13A5 5 0 1 0 15 13M12 4A1 1 0 0 1 13 5V8H11V5A1 1 0 0 1 12 4Z" />
              </svg>
            </div>
          </div>
          <div class="card-content">
            <div class="value-group">
              <div class="value">{{ Math.round(weatherInfo?.main.feels_like) }}<span class="unit">°C</span></div>
            </div>
          </div>
        </section>

        <!-- Sunrise/Sunset -->
        <section class="card">
          <div class="card-header">
            <div class="card-title">Sun Cycle</div>
            <div class="card-icon">
              <svg viewBox="0 0 24 24" class="tactical-icon">
                <path d="M3,12H7A5,5 0 0,1 12,7A5,5 0 0,1 17,12H21A1,1 0 0,1 22,13A1,1 0 0,1 21,14H3A1,1 0 0,1 2,13A1,1 0 0,1 3,12M15,12A3,3 0 0,0 12,9A3,3 0 0,0 9,12H15M12,2L14.39,5.42C13.65,5.15 12.84,5 12,5C11.16,5 10.35,5.15 9.61,5.42L12,2M3.34,7L7.5,6.65C6.9,7.16 6.36,7.78 5.94,8.5C5.5,9.24 5.25,10 5.11,10.79L3.34,7M20.65,7L18.88,10.79C18.74,10 18.47,9.23 18.05,8.5C17.63,7.78 17.1,7.15 16.5,6.64L20.65,7M12.71,16.3L15.82,19.41C16.21,19.8 16.21,20.43 15.82,20.82C15.43,21.21 14.8,21.21 14.41,20.82L12,18.41L9.59,20.82C9.2,21.21 8.57,21.21 8.18,20.82C7.79,20.43 7.79,19.8 8.18,19.41L11.29,16.3C11.68,15.91 12.31,15.91 12.71,16.3Z" />
              </svg>
            </div>
          </div>
          <div class="card-content sun-times">
            <div class="sun-time">
              <span class="label">Rise</span>
              <span class="time">{{ sun(weatherInfo?.sys.sunrise, weatherInfo?.timezone) }}</span>
            </div>
            <div class="sun-time">
              <span class="label">Set</span>
              <span class="time">{{ sun(weatherInfo?.sys.sunset, weatherInfo?.timezone) }}</span>
            </div>
          </div>
        </section>

        <!-- Cloudiness -->
        <section class="card">
          <div class="card-header">
            <div class="card-title">Cloudiness</div>
            <div class="card-icon">
              <svg viewBox="0 0 24 24" class="tactical-icon">
                <path d="M6,19A5,5 0 0,1 1,14A5,5 0 0,1 6,9C7,6.65 9.3,5 12,5C15.43,5 18.24,7.66 18.5,11.03L19,11A3,3 0 0,1 22,14A3,3 0 0,1 19,17H13V19A1,1 0 0,1 12,20A1,1 0 0,1 11,19V17H6M12,11H15V8L18.4,11.4L15,14.8V12H12V15L8.6,11.6L12,8.2V11Z" />
              </svg>
            </div>
          </div>
          <div class="card-content">
            <div class="value-group">
              <div class="value">{{ weatherInfo?.clouds.all }}<span class="unit">%</span></div>
            </div>
          </div>
        </section>
      </div>
    </div>
  </main>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'

@keyframes border-run
  0%
    background-position: 0% center
  100%
    background-position: 200% center

@keyframes tactical-scan
  0%
    transform: translateY(-100%)
    opacity: 0.3
  100%
    transform: translateY(100%)
    opacity: 0

.highlights
  padding: 20px
  background: rgba(7, 8, 3, 0.6)
  border-radius: 16px
  position: relative
  &::before
    content: ''
    position: absolute
    inset: 0
    border-radius: 16px
    padding: 2px
    background: linear-gradient(90deg, #7BFF00, #304C02, #7BFF00)
    -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0)
    -webkit-mask-composite: destination-out
    mask-composite: exclude
    background-size: 200% auto
    animation: border-run 4s linear infinite

.title
  color: #7BFF00
  font-size: 18px
  margin-bottom: 20px
  text-transform: uppercase
  letter-spacing: 1px

.highlights-grid
  display: grid
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr))
  gap: 16px

.card
  background: rgba(18, 26, 15, 0.9)
  border-radius: 8px
  padding: 16px
  position: relative
  overflow: visible
  backdrop-filter: blur(10px)
  transition: all 0.3s ease
  transform-style: preserve-3d
  perspective: 1000px

  &::before
    content: ''
    position: absolute
    inset: 0
    border-radius: 8px
    padding: 1px
    background: linear-gradient(90deg, #7BFF00, #304C02, #7BFF00)
    -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0)
    -webkit-mask-composite: destination-out
    mask-composite: exclude
    background-size: 200% auto
    animation: border-run 4s linear infinite
    opacity: 0.6

  &::after
    content: ''
    position: absolute
    inset: 0
    background: linear-gradient(125deg, rgba(123, 255, 0, 0.2) 0%, rgba(0, 0, 0, 0) 60%)
    opacity: 0
    transition: opacity 0.3s ease
    pointer-events: none

  &:hover
    transform: translateY(-2px)
    background: rgba(18, 26, 15, 0.95)
    &::before
      opacity: 1
    &::after
      opacity: 1

.card-header
  display: flex
  justify-content: space-between
  align-items: center
  margin-bottom: 16px

.card-title
  color: #7BFF00
  font-size: 14px
  text-transform: uppercase
  letter-spacing: 1px
  &::before
    content: '['
    margin-right: 4px
    opacity: 0.5
  &::after
    content: ']'
    margin-left: 4px
    opacity: 0.5

.card-icon
  width: 24px
  height: 24px

.tactical-icon
  fill: #7BFF00
  opacity: 0.8
  transition: all 0.3s ease
  &:hover
    opacity: 1
    transform: scale(1.1)

.value-group
  display: flex
  flex-direction: column
  gap: 8px

.value
  color: #7BFF00
  font-size: 24px
  font-family: 'Inter', monospace
  text-shadow: 0 0 10px rgba(123, 255, 0, 0.3)

.unit
  font-size: 14px
  margin-left: 4px
  opacity: 0.7

.sun-times
  display: grid
  grid-template-columns: 1fr 1fr
  gap: 12px

.sun-time
  display: flex
  flex-direction: column
  align-items: center
  
  .label
    color: rgba(123, 255, 0, 0.7)
    font-size: 12px
    text-transform: uppercase
    margin-bottom: 4px
  
  .time
    color: #7BFF00
    font-size: 14px
    font-family: 'Inter', monospace
    text-shadow: 0 0 10px rgba(123, 255, 0, 0.3)

.card-tooltip
  position: absolute
  bottom: calc(100% + 16px)
  left: 50%
  transform: translateX(-50%) translateY(10px)
  background: rgba(7, 8, 3, 0.95)
  padding: 16px
  border-radius: 8px
  opacity: 0
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1)
  pointer-events: none
  z-index: 10
  backdrop-filter: blur(10px)
  width: 280px
  visibility: hidden
  display: flex
  gap: 16px
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.5)
  
  &::before
    content: ''
    position: absolute
    bottom: -8px
    left: 50%
    transform: translateX(-50%)
    border-left: 8px solid transparent
    border-right: 8px solid transparent
    border-top: 8px solid rgba(7, 8, 3, 0.95)
  
  &::after
    content: ''
    position: absolute
    inset: 0
    border-radius: 8px
    padding: 1px
    background: linear-gradient(90deg, #7BFF00, #304C02, #7BFF00)
    -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0)
    -webkit-mask-composite: destination-out
    mask-composite: exclude
    pointer-events: none
    animation: border-run 4s linear infinite
    background-size: 200% auto

.card
  &:hover
    .card-tooltip
      opacity: 1
      transform: translateX(-50%) translateY(0)
      visibility: visible
      pointer-events: auto

.tooltip-image
  width: 80px
  height: 80px
  object-fit: cover
  border-radius: 4px
  border: 1px solid rgba(123, 255, 0, 0.3)
  transition: all 0.3s ease
  
  &:hover
    transform: scale(1.05)
    border-color: rgba(123, 255, 0, 0.8)
    box-shadow: 0 0 15px rgba(123, 255, 0, 0.2)

.tooltip-content
  flex: 1

  h3
    color: #7BFF00
    font-size: 12px
    text-transform: uppercase
    letter-spacing: 1px
    margin-bottom: 8px
    font-family: 'Inter', monospace
    display: flex
    align-items: center
    gap: 8px
    text-shadow: 0 0 10px rgba(123, 255, 0, 0.3)
    
    &::before
      content: '>'
      color: #7BFF00
      opacity: 0.5
    
  p
    color: rgba(123, 255, 0, 0.8)
    font-size: 12px
    line-height: 1.4
    margin: 0

@media (max-width: 768px)
  .highlights-grid
    grid-template-columns: repeat(2, 1fr)

@media (max-width: 480px)
  .highlights-grid
    grid-template-columns: 1fr
</style>
