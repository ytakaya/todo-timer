<template>
  <div class="timer">
    <h2>{{ title_group }} <input v-model="title_group" type="text"></h2>
    <ul>
      <li v-for="timer of timers" :key="timer.id">
        <Timer :timer_id="timer.id"
               @removeTimer="removeTimer" 
        />
      </li>
      <li>
        <button v-on:click="addTimer()">+</button>
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
      timers: [
        {id: 0}
      ],
      next_id: 1,
      title_group: "",
    }
  },
  methods: {
    addTimer() {
      this.timers.push({
        id: this.next_id,
      })
      this.next_id += 1;
    },
    removeTimer(timer_id) {
      for (let i=0; i<this.timers.length; i++) {
        if (this.timers[i].id === timer_id) {
          this.timers.splice(i, 1);
          return
        }
      }
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