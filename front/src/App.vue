<template>
  <div id="app">
    <TimerGroup/>
    <TimerGroup/>
  </div>
</template>

<script>
import TimerGroup from './components/TimerGroup.vue'

export default {
  name: 'App',
  components: {
    TimerGroup
  }
}
</script>

<style>
.clear {
  clear: both;
}
</style>
