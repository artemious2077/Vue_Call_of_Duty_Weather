<script setup>
import { getPresure, sun } from "../utils/utils";

const props = defineProps({
  weatherInfo: {
    required: true,
    type: [Object, null],
  },
});

</script>

<template>
  <main class="section highlights">
    <div class="title">Today's Highlights</div>
    <div class="highlights-wrapper">
      <section class="highlight">
        <section class="card">
          <div class="card-title">Wind</div>
          <div class="card-pic card-pic--wind"></div>
          <article class="card-info">
            <div class="card-justify">
              <div class="info-main">
                <p class="info-main-num">
                  {{ weatherInfo?.wind.speed }}
                </p>
                <p class="info-main-text">m/s</p>
              </div>
              <div class="info-main">
                <p class="info-main-num">
                  {{ weatherInfo?.wind.deg }}
                </p>
                <p class="info-main-text">deg</p>
              </div>
            </div>
          </article>
        </section>
        <div class="card-small">
          <h2 class="card-small-title">Wind gusts</h2>
          <div class="card-small-info">
            <div class="card-small-data">
              <p class="info-main-num">
                {{ weatherInfo?.wind.gust }}
              </p>
              <div class="info-main-text">m/s</div>
            </div>
            <article class="card-small-hint">
              <div class="card-small-pic card-small-pic--wind"></div>
              <p class="card-small-text text-egorova">
                Learn
                <a
                  href="https://www.windy.com/articles/weather-phenomena-what-s-the-difference-between-sustained-winds-and-wind-gusts-10390?satellite,7.787,115.115,5"
                  target="_blank"
                  >more</a
                >
                about gusts
              </p>
            </article>
          </div>
        </div>
      </section>
      <section class="highlight">
        <article class="card">
          <div class="card-title">Pressure</div>
          <div class="card-pic card-pic--pressure"></div>
          <div class="card-info">
            <div class="card-centered">
              <div class="info-main">
                <p class="info-main-num">
                  {{ getPresure(weatherInfo?.main.pressure) }}
                </p>
                <div class="info-main-text">mm</div>
              </div>
            </div>
          </div>
        </article>
        <article class="card-small">
          <div class="card-small-title">Feels like</div>
          <div class="card-small-info">
            <div class="card-small-data">
              <p class="info-main-num">
                {{ Math.round(weatherInfo?.main.feels_like) }}
              </p>
              <div class="info-main-text">°C</div>
            </div>
            <div class="card-small-hint">
              <div
                class="card-small-pic card-small-pic--margin card-small-pic--pressure"
              ></div>
              <p class="card-small-text">How hot or cold it really feels</p>
            </div>
          </div>
        </article>
      </section>
      <div class="highlight">
        <section class="card">
          <h2 class="card-title">Sunrise and sunset</h2>
          <div class="card-pic card-pic--sun"></div>
          <section class="card-info">
            <div class="states">
              <article class="state">
                <div class="state-pic"></div>
                <p class="state-title">Sunrise</p>
                <p class="state-time">
                  {{ sun(weatherInfo?.sys.sunrise, weatherInfo?.timezone) }}
                </p>
              </article>
              <article class="state">
                <div class="state-pic state-pic--flipped"></div>
                <p class="state-title">Sunset</p>
                <p class="state-time">
                  {{ sun(weatherInfo?.sys.sunset, weatherInfo?.timezone) }}
                </p>
              </article>
            </div>
          </section>
        </section>
        <section class="card-small">
          <p class="card-small-title">Cloudiness</p>
          <section class="card-small-info">
            <article class="card-small-data">
              <p class="info-main-num">
                {{ weatherInfo?.clouds.all }}
              </p>
              <div class="info-main-text">%</div>
            </article>
            <article class="card-small-hint">
              <aside class="card-small-pic card-small-pic--sun"></aside>
              <p class="card-small-text">
                The sky fraction obscured by clouds
              </p>
            </article>
          </section>
        </section>
      </div>
    </div>
  </main>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'

.highlights
  padding: 28px 16px 16px
  background: #070803
  border: 2px solid #32392D
  border-radius: 25px

  &-wrapper
    display: flex
    justify-content: space-between

    @media (max-width: 575px)
      flex-direction: column

.title
  padding-bottom: 16px

.highlight
  width: 32%

  @media (max-width: 575px)
    width: 100%
    margin-bottom: 16px

.card
  min-height: 230px
  padding: 16px
  border-radius: 8px
  background: radial-gradient(#121A0F,#403825)
  border: 2px solid #A8D432

  @media (max-width: 1199px)
    padding: 12px

  &-centered
    display: flex
    justify-content: center
    margin-top: 40px

  &-justify
    display: flex
    justify-content: space-between
    margin-top: 40px

  &-title
    padding-bottom: 12px
    font-size: 13px

    @media (max-width: 1199px)
      font-size: 12px

  &-pic
    width: 100%
    height: 80px
    margin-bottom: 16px
    background-repeat: no-repeat
    background-position: 50% 50%
    background-size: contain

    &--wind
      background-image: url('/src/assets/img/wind.webp')

    &--pressure
      background-image: url('/src/assets/img/fuss-aneometr.png')

    &--sun
      background-image: url('/src/assets/img/sunMoving.png')


.states
  display: flex
  justify-content: space-between

  &--margin
    margin-top: 40px

.state
  width: 40%

  &:last-child
    text-align: right

  &-pic
    width: 20px
    height: 20px
    margin-bottom: 6px
    background: url('/src/assets/img/sun.svg') no-repeat 50% 50%
    background-size: cover

    &--flipped
      margin-left: auto
      -webkit-transform: scaleX(-1)
      transform: scaleX(-1)

  &-title
    font-size: 12px
    color: $gold

  &-time
    font-size: 13px
    font-weight: 700

    @media (max-width: 1199px)
      font-size: 11px

.info-main
  display: flex
  align-items: flex-end

  &:last-child
    text-align: right

  &-num
    font-size: 20px

    @media (max-width: 1199px)
      font-size: 18px

  &-text
    padding-left: 2px
    padding-bottom: 3px
    font-size: 13px
    color: rgba($white, 0.75)

    @media (max-width: 1199px)
      padding-bottom: 1.5px
      font-size: 12px

.card-small
  margin-top: 12px
  padding: 12px 16px
  background: #070803
  border: 2px solid #32392D
  border-radius: 8px
  transition: 0.2s
  &:hover 
    background: #67861B
    border: 2px solid #67861B

  &-title
    font-size: 13px

  &-info
    display: flex
    justify-content: space-between
    align-items: center

    @media (max-width: 1199px)
      flex-direction: column
      align-items: flex-start

  &-pic
    width: 20px
    height: 20px
    background-repeat: no-repeat
    background-position: 50% 50%
    background-size: contain

    @media (max-width: 1199px)
      display: none

    &--margin
      width: 16px
      height: 16px
      margin-bottom: 3px

    &--wind
      background-image: url('/src/assets/img/gusts.svg')

    &--pressure
      background-image: url('/src/assets/img/humidity.svg')

    &--sun
      background-image: url('/src/assets/img/cloud.svg')

  &-data
    display: flex
    align-items: flex-end
    width: 45%

    @media (max-width: 1199px)
      width: 100%
      padding-top: 8px

  &-hint
    width: 55%

    @media (max-width: 1199px)
      width: 100%

  &-text
    font-size: 11px
    line-height: 1.2
    color: rgba($white, 0.6)

    @media (max-width: 1199px)
      min-height: 22px
      font-size: 9px
</style>
