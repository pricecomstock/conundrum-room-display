<template>
  <div id="timer">
      {{formattedTime}}
  </div>
</template>

<script>
export default {
  name: 'timer',
  props: {
      secondsRemaining: {
          type: Number,
          default: 754
      }
  },
  computed: {
      formattedTime() {
          let minutes = Math.floor(this.secondsRemaining / 60);
          let seconds = this.secondsRemaining % 60;
          return `${minutes.toString().padStart(2,'0')}:${seconds.toString().padStart(2,'0')}`
      }
  },
  data () {
    return {
    }
  }
}
</script>

<style lang="scss">

#timer {
    color: white;
    font-size: 15em;
    font-family: "OpenSans";
    font-weight: 700;
    padding: 0;
    margin: 0;
    position: fixed;
    bottom: 30%;
    left: 30px;
}
</style>
