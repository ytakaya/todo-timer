<template>
  <div class="timer">
    <div v-if="title_input">
      <input ref="timerInput" v-model="timer_info" @blur="title_input=false" @keyup.enter="title_input=false; registerInfo()" type="text">
    </div>
    <div v-else>
      <h3 @click="timerInput()">{{ title }} <button v-on:click="removeTimer()">x</button></h3>
    </div>

    <p class="time-font">{{ formatedTime }}</p>
    <button v-on:click="start()">start</button>
    <button v-on:click="stop()">stop</button>
  </div>
</template>

<script>
export default {
  props: {
    timer_id: Number
  },
  data: function() {
    return {
      id: null,
      timer_info: 'NoTitle 0',
      title_input: false,
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
    timerInput() {
      this.title_input=true;
      this.$nextTick(() => {this.$refs.timerInput.focus();})
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
    },
    removeTimer() {
      this.$emit("removeTimer", this.timer_id)
    }
  }
}
</script>

<style scoped>
.time-font {
  font-size: 32px;
  margin: 10px 0;
}
h3 {
  margin-top: 0;
}
.timer {
  border: solid 1px gray;
  padding: 20px;
}
</style>