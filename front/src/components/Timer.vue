<template>
  <div class="hello">
    <p>{{ time }}</p>
    <button v-on:click="start()">start</button>
    <button v-on:click="stop()">stop</button>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      time: 3000,
      id: null,
    }
  },
  methods: {
    start() {
      this.id = setInterval(() => {
        this.time -= 1
      }, 1000)
    },
    stop() {
      clearInterval(this.id);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
