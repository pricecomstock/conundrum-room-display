<template>
  <div id="app">
    <div class="section">
    	<div class="columns">
    	  <div class="column is-9">
    	    <div class="hero is-black is-medium timercontainer">
            <div class="hero-body">
              <div class="container">
                <timer :seconds-remaining="room.secondsRemaining"></timer>
              </div>
            </div>
          </div>
    	  </div>
    	    <hint-list class="column is-3" v-if="room.hints" :hints="room.hints"></hint-list>
    	</div>
    </div>
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

#app {
  background-color: #000;
}

.timercontainer {
  padding: 6% 0%
}
</style>
