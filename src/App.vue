<template>
  <v-layout id="app" row wrap>
    <v-flex xs12 sm10 offset-sm1 fill-height>
      <v-card-text class="time-right">{{this.getTime }}</v-card-text>
      <v-card class="progress-bar">
        <v-card-title class="app-title">***Last-Man Standing***</v-card-title>
        <v-spacer></v-spacer>

        <h4 class="text">$ Defeat the Boss $</h4>
        <v-spacer></v-spacer>

        <v-card-text>Game Session: {{ this.sessionDisplay() }}</v-card-text>
      </v-card>
      <v-spacer></v-spacer>
      <v-card>
        <v-card-text >
          <!-- <span> {{ this.countDown }}</span> <br /> -->

          <v-btn flat color="blue" @click="this.countDown" v-if="!gameStart"> Begin Game</v-btn>
        </v-card-text>
      </v-card>

      <Playground v-if="gameStart" />
    </v-flex>
  </v-layout>
</template>

<script>
import Playground from "./components/playground";
// add restart button later
//  add logic for when player wins or looses;
// add logic for closing game once timer ends

export default {
  name: "app",
  components: {
    Playground
  },
  data() {
    return {
      // implement countdown with js - done
      countDownValue: 120,
      sessionTime: 240,
      gameStart: false
    };
  },
  methods: {
    sessionDisplay: function(){
      let countDownTime = parseInt(this.sessionTime);
      // console.log(typeof(this.sessionTime));
      let min = parseInt(countDownTime/60);
      let sec = parseInt(countDownTime % 60);
      let output = this.formatTime(min)+':'+ this.formatTime(sec);
      // console.log(output);
      return output;

    },
    countDown: function() {
      this.gameStart = true;
      // console.log(this.gameStart);

      if(this.sessionTime){
        let newValue = parseInt(this.sessionTime);

        setInterval(()=>{
          // console,log(newValue);
          let limit = 0;
          while (newValue !== limit) {
            newValue = newValue - 1;
            // console.log(newValue);
            this.sessionTime = newValue;
            if(this.sessionTime === limit) {
              this.gameStart = false;
            }
            // startValue = newValue;
            return this.sessionTime;
          }
        }, 1000);
      } 
    },
    formatTime(digits){
      
      let numbers = new String(digits);
      // console.log(numbers);
      if(numbers.length >1){
        // console.log(digits);
        return digits;
      } else {
        // console.log(digits);
        let formatedStr = '0'+ digits;
        // console.log(formatedStr);
        return formatedStr;
      }
    }

  },
  computed: {
    getTime: function() {
      let current = new Date();
      let localTime = current.toDateString();
      return localTime;
    }

  }
};
</script>

<style >
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  align-items: center;
  padding: 0.5vh;
  vertical-align: center;
}
.app-title {
  padding-bottom: 30px;
  justify-content: center;
  font-size: 2.4em;
  font-weight: 400;
}
.progress-bar {
  padding-top: 30px;
  padding-bottom: 30px;
  font-size: 1.3em;
}
.time-right {
  text-align: end;
}
</style>
