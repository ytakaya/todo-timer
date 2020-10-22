<template>
  <div class="timer">
    <ul>
      <li v-for="timer in timers" :key="timer.title"><Timer :title="timer.title" :time="timer.time" /></li>
      <div class="clear"></div>
    </ul>
  </div>
</template>

<script>
import Timer from './Timer.vue'

export default {
  components: {
    Timer
  },
  data: () => {
    return {
      timers: [
        {title: 'sample1', time: 300},
        {title: 'sample2', time: 400}
      ]
    }
  }
}
</script>

<style scoped>
li {
  list-style: none;
  float: left;
  margin-right: 10px;
}
</style>