<template>
  <div id="app">
    <div class="bg"></div>
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
@font-face {
    font-family: "FinalFrontier";
    src: url($font_path + 'finalfrontier.ttf');
}
@font-face {
    font-family: "LCARS";
    src: url($font_path + 'lcars.ttf');
}
@font-face {
    font-family: "LCARS";
    src: url($font_path + 'lcarsbold.ttf');
    font-weight: bold;
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
</style>
