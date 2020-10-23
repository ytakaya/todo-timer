<template>
  <div id="timer-view">
    <ul>
      <li v-for="n of num_groups" :key="n"><TimerGroup /></li>
      <li>
        <button v-on:click="add_group()">+</button>
      </li>
    </ul>
  </div>
</template>

<script>
import TimerGroup from './TimerGroup.vue'

export default {
  components: {
    TimerGroup
  },
  data: () => {
    return {
      num_groups: 1,
    }
  },
  methods: {
    add_group() {
      this.num_groups += 1;
      return 0
    }
  }
}
</script>

<style scoped>
</style>
