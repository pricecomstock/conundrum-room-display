<template>
  <div id="app">
    <!-- <div class="fullscreen-bg">
      <video loop muted autoplay poster="./assets/stars.jpg" class="fullscreen-bg__video">
          <source src="./assets/test.mp4" type="video/mp4">
      </video>
    </div> -->
    <timer :seconds-remaining="room.secondsRemaining"></timer>
    <hint-list></hint-list>
    <!-- <puzzle-status :puzzles="room.puzzles"></puzzle-status> -->
  </div>
</template>

<script>
import axios from './axios-roomcontroller'
import Timer from './components/Timer.vue'
import HintList from './components/HintList.vue'
import PuzzleStatus from './components/PuzzleStatus.vue'
export default {
  name: 'app',
  components: {
    timer: Timer,
    puzzleStatus: PuzzleStatus,
    hintList: HintList
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
    font-family: "OpenSans";
    src: url($font_path + 'OpenSans-Regular.ttf');
    font-weight: 400;
}

@font-face {
    font-family: "OpenSans";
    src: url($font_path + 'OpenSans-Bold.ttf');
    font-weight: 700;
}

@font-face {
    font-family: "OpenSans";
    src: url($font_path + 'OpenSans-ExtraBold.ttf');
    font-weight: 800;
}

@font-face {
    font-family: "OpenSans";
    src: url($font_path + 'OpenSans-SemiBoldItalic.ttf');
    font-weight: 600;
    font-style: italic;
}

// .bg {
//   position: absolute;
//   left: 0;
//   right: 0;
//   top: 0;
//   bottom: 0;
//   z-index: -1;
//   background-image: url('./assets/bg.jpg');
//   background-size: 130%;
//   overflow: visible;
// }

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
  background-color: #000;
}
</style>
