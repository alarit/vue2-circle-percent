<template>
  <div id="app">
      <div class="one-fourth">
          <circular-percentage :size="size" :done="3" :missing="1" arcColor="#0000ff" bgCircleColor="#0000bb33" />
      </div>
      <div class="one-fourth">
        <circular-percentage size="80" :done="60" :missing="30" arcColor="#ff0000" bgCircleColor="#ff000033" />
      </div>
      <div class="one-fourth">
        <circular-percentage size="60" :done=done :missing=missing />
      </div>
      <div class="one-fourth">
          <circular-percentage size="40" :done="90" :missing="10" arcColor="#fff000" bgCircleColor="#fff00033" />
      </div>
  </div>
</template>

<script>
import CircularPercentage from './components/CircularPercentage.vue'

export default {
  name: 'app',
  components: {
      CircularPercentage
  },
    data() {
        return {
            size: 100,
            done: 5,
            missing: 20
      }
    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}

.one-fourth {
    width: 25%;
    float: left;
}
</style>
