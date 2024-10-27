<template>
  <div class="timer">
    {{ minutes }}:{{ seconds }}
  </div>
</template>

<script>
export default {
  name: "Timer",
  data() {
    return {
      totalSeconds: 0,
      interval: null
    }
  },
  computed: {
    minutes() {
      return Math.floor(this.totalSeconds / 60)
        .toString()
        .padStart(2, '0')
    },
    seconds() {
      return (this.totalSeconds % 60)
        .toString()
        .padStart(2, '0')
    }
  },
  methods: {
    start() {
      this.interval = setInterval(() => {
        this.totalSeconds++
      }, 1000)
    },
    stop() {
      clearInterval(this.interval)
    }
  },
  created() {
    this.start()
  },
  beforeDestroy() {
    clearInterval(this.interval)
  }
}
</script>

<style scoped>
  .timer {
    font-size: 2rem;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    text-align: right;
  }

  button {
    margin-left: 1rem;
    padding: 0.5rem 1rem;
  }
</style>