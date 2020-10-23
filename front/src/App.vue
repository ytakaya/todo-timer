<template>
  <div id="app">
    <TimerView />
  </div>
</template>

<script>
import TimerView from './components/TimerView.vue'

export default {
  name: 'App',
  components: {
    TimerView
  },
}
</script>

<style>
.clear {
  clear: both;
}ul {
  padding: 0;
}
li {
  list-style: none;
}
</style>
