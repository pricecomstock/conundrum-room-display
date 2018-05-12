<template>
  <div id="app">
    <!-- <div class="fullscreen-bg">
      <video loop muted autoplay poster="./assets/stars.jpg" class="fullscreen-bg__video">
          <source src="./assets/test.mp4" type="video/mp4">
      </video>
    </div> -->
    <timer :seconds-remaining="room.secondsRemaining"></timer>
    <puzzle-status :puzzles="room.puzzles"></puzzle-status>
  </div>
</template>

<script>
import axios from './axios-roomcontroller'
import Timer from './components/Timer.vue'
import PuzzleStatus from './components/PuzzleStatus.vue'
export default {
  name: 'app',
  components: {
    timer: Timer,
    puzzleStatus: PuzzleStatus
  },
  data () {
    return {
      room: {}
    }
  },
  created() {
    setInterval(() => {
      axios.get('/room')
      .then(response => {
        console.log(response)
        this.room = response.data;
      })
    }, 500)
  }
}
</script>

<style lang="scss">
$font_path: './assets/fonts/';

@keyframes moveBackground {
   0% {
     background-size: 130%;
   }
   50% { 
     background-size: 132%;
   }
   100% { 
     background-size: 130%;
   }
}

@font-face {
    font-family: "FiraCode";
    src: url($font_path + 'FiraCode-Regular.ttf');
}

.bg {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  z-index: -1;
  background-image: url('./assets/stars.jpg');
  background-size: 130%;
  overflow: visible;

  // animation-name: moveBackground;
  // animation-duration: 100s;
  // animation-iteration-count: infinite;
  // animation-timing-function: ease-in-out;
}

.fullscreen-bg {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  overflow: hidden;
  z-index: -100;
}

.fullscreen-bg__video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

body {
  background-color: black;
}
</style>
