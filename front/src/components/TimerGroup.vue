<template>
  <div class="timer">
    <h2>{{ title_group }} <input v-model="title_group" type="text"></h2>
    <ul>
      <li v-for="i of num_timers" :key="i"><Timer /></li>
      <li>
        <button v-on:click="add_timer()">+</button>
      </li>
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
      num_timers: 1,
      title_group: "",
    }
  },
  methods: {
    add_timer() {
      this.num_timers += 1;
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