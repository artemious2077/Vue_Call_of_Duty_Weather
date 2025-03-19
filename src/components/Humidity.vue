<script setup>

const props = defineProps({
  weatherInfo: {
    required: true,
    type: [Object, null],
  }
})

</script>

<template>
  <main class="block-bottom">
    <section class="block-bottom-inner">
      <div class="block-bottom-pic pic-humidity"></div>
      <div class="block-bottom-texts">
        <article class="block-bottom-text-block">
          <p class="block-bottom-text-block-title">
            Humidity: {{ weatherInfo?.main.humidity }} %
          </p>
          <span class="block-bottom-text-block-desc">
            Humidity is the concentration of water vapor present in the air. Water vapor, the gaseous state of
            water, is generally invisible to the human eye.
            <br /><br />
            The same amount of water vapor results in higher relative humidity in cool air than warm air.
          </span>
        </article>
      </div>
    </section>
  </main>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'
</style>