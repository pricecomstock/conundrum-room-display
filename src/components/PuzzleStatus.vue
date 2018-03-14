<template>
  <div id="puzzlestatus">
      <div class="statustitle">VESSEL STATUS 038491</div>
      <table v-if="this.puzzles">
          <!-- <tr>
              <th>System</th>
              <th>Status</th>
          </tr> -->
          <template v-for="(value, key, index) in prettyPuzzles">
            <tr :key="key">
                <th>{{key}}</th>
                <td v-for="n in numberExtraColumns" :key="n" style="text-align: right">
                    {{ randomNums[index*numberExtraColumns + n] }}
                </td>
                <td>{{value}}</td>
            </tr>
          </template>
      </table>
  </div>
</template>

<script>
export default {
  name: 'puzzlestatus',
  props: {
      puzzles: {
        //   type: Object,
        //   required: true
      }
  },
  computed: {
      prettyPuzzles() {
          let prettyPuzzles = Object.keys(this.puzzles).reduce( (accumulator, key) => {
            let niceName = this.puzzleDict[key].name
            let niceStatus = this.puzzles[key] ? this.puzzleDict[key].trueStatus : this.puzzleDict[key].falseStatus
            accumulator[this.puzzleDict[key].name] = niceStatus
            return accumulator
          }, {});
          return prettyPuzzles
      }
  },
  data () {
    return {
         puzzleDict: {
            "lifesupport": {
                name: "Life Support",
                trueStatus: "Online",
                falseStatus: "Offline"
            },
            "fuelcells": {
                name: "Fuel Cells",
                trueStatus: "Disconnected",
                falseStatus: "Connected"
            },
            "fusiondrive": {
                name: "Fusion Drive",
                trueStatus: "Enabled",
                falseStatus: "Disabled"
            },
            "navigation": {
                name: "Navigation Systems",
                trueStatus: "Online",
                falseStatus: "Offline"
            },
            "plottedcourse": {
                name: "Destination",
                trueStatus: "Unknown",
                falseStatus: "Locked"
            }
         },
         randomNums: [0,0],
         numberExtraColumns: 6
    }
  },
  methods: {
      generateRandomNumberString() {
          const bucket = Math.random() // we want an aesthetic distribution, not a uniform one
          if (bucket <= 0.05) { // BLANK
              return ""
          } else if (bucket <= 0.3) { // UP TO 2 DIGITS
              return Math.floor(Math.random()*99).toString();
          } else if (bucket <= 0.8) { // UP TO 4 DIGITS
              return Math.floor(Math.random()*9999).toString();
          } else { // UP TO SIX DIGITS
              return Math.floor(Math.random()*999999).toString();
          }
      }
  },
  created() {
      const blankArray = Array(this.numberExtraColumns * 5).fill(0)
      this.randomNums = blankArray.map(this.generateRandomNumberString)
  }
}
</script>

<style lang="scss">
$st_darkyellow: #fe9a07;
$st_burntorange: #ff5f2d;
$st_lightindigo: #999bff;
$st_violet: #d19ad1;
$st_red: #ce605f;
$st_tan: #fdc379;
$st_white: #fef4f1;

#puzzlestatus {
    color: white;
    font-size: 35px;
    font-family:'LCARS';
    padding: 0;
    margin: 0;
    position: fixed;
    top: 10px;
    right: 30px;
    text-transform: uppercase;
    border-bottom: $st_lightindigo 25px solid;
    border-left: $st_lightindigo 85px solid;
    border-bottom-left-radius: 120px 70px;
}

.statustitle {
    font-size: 80px;
    text-align: right;
    color: $st_darkyellow;
}

table {
    border-spacing: 30px 0px;
}

th {
    text-align: right;
}
</style>
