<template>
  <div class="group">
    <input type="text" v-model="title">
    <h3>{{ title }}</h3>
    <p class="time-font">{{ formatedTime }}</p>
    <button v-on:click="start()">start</button>
    <button v-on:click="stop()">stop</button>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      id: null,
      title: 'sample1',
      time: 300,
    }
  },
  computed: {
    formatedTime() {
      var hms = "";
      var h = this.time / 3600 | 0;
      var m = this.time % 3600 / 60 | 0;
      var s = this.time % 60;

      if (h != 0) {
        hms = `${h}:${padZero(m)}:${padZero(s)}`;
      } else if (m != 0) {
        hms = m + ":" + padZero(s);
      } else {
        hms = s;
      }

      return hms;

      function padZero(v) {
        if (v < 10) {
          return "0" + v;
        } else {
          return v;
        }
      }
    }
  },
  methods: {
    start() {
      if (!this.id) {
        this.id = setInterval(() => {
          this.time -= 1
        }, 1000)
      }
    },
    stop() {
      clearInterval(this.id);
      this.id = null;
    }
  }
}
</script>

<style scoped>
.time-font {
  font-size: 32px;
}
</style>