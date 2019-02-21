<template>
  <section class="container">
    <div>
      <h1 class="title">amenoha</h1>
      <h2 class="subtitle">昨日の天気と比べてどうすれば過ごしやすいか教えてくれるアプリ</h2>
      <Weather />
    </div>
  </section>
</template>

<script>
import Weather from '~/components/Weather.vue'

export default {
  components: {
    Weather
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 30px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 16px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

</style>
