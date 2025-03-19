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
    <div class="block-bottom-inner">
      <div class="block-bottom-pic pic-coords"/>
      <section class="block-bottom-texts">
        <article class="block-bottom-text-block">
          <p class="block-bottom-text-block-title">
            Longitude: {{ weatherInfo?.coord.lon }}
          </p>
          <p class="block-bottom-text-block-desc">
            Longitude measures distance east or west of the prime meridian.
          </p>
        </article>
        <article class="block-bottom-text-block">
          <p class="block-bottom-text-block-title">
            Latitude: {{ weatherInfo?.coord.lat }}
          </p>
          <p class="block-bottom-text-block-desc">
            Latitude lines start at the equator (0 degrees latitude) and run east and west, parallel to the
            equator.
          </p>
        </article>
      </section>
    </div>
  </main>
</template>

<style lang="sass" scoped>
@import '../assets/styles/main'
</style>