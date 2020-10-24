<template>
  <div class="group">
    <input type="text" v-on:keyup.enter="registerInfo()" v-model="timer_info">
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
      timer_info: '',
      title: "NoTitle",
      time: 0,
      unit: 1,
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
    },
  },
  methods: {
    start() {
      if (!this.id) {
        this.id = setInterval(() => {    
         this.time += this.unit
        }, 1000)
      }
    },
    stop() {
      clearInterval(this.id);
      this.id = null;
    },
    registerInfo() {
      const info_arr = this.timer_info.split(' ');
      this.title = info_arr[0];
      if (info_arr.length > 1) {
        if (info_arr[info_arr.length - 1] === '0') {
          this.unit = 1; 
        }
        else {
          this.time = Number(info_arr[info_arr.length - 1]);
          this.unit = -1;
        }
      }
    }
  }
}
</script>

<style scoped>
.time-font {
  font-size: 32px;
  margin: 10px 0;
}
</style>