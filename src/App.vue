<template>
  <div class="game">
    <div class="main-content">
      <Highscores :totalScore="totalScore"></Highscores>
      
      <div class="heading-container">
        <h1 class="game-title">Reaction-ary</h1>
      </div>
      
      <SpeedCounter :class="{ 'pause': isDissolving, 'animate': counterStatus }"></SpeedCounter>
      
      <Results v-if="showResults" :score="score" />
      
      <Instructions :class="{ 'hide': exitHome }"></Instructions>
      
      <Shadow v-if="isDissolving"></Shadow>
      
      <Protester v-if="isPlaying" class="playing" :class="{ 'dissolving': isDissolving }" :delay="delay+200" @stop="stopGame" @click="dissolveProtester" @timerOn="startCounter"/>
      
      <button class="start" @click="start" :disabled="isPlaying">Start</button>
    </div>
    <div class="background-content">
      <Protester v-if="atHome" class="home" :class="{ 'hide': exitHome }"/>
    </div>
  </div>
</template>

<script>
import Protester from './components/Protester.vue'
import Results from './components/Results.vue'
import Instructions from './components/Instructions.vue'
import Shadow from './components/Shadow.vue'
import Highscores from './components/Highscores.vue'
import SpeedCounter from './components/SpeedCounter.vue'
export default {
  name: 'App',
  components: { Protester, Results, Instructions, Shadow, Highscores, SpeedCounter },
  data() {
    return {
      atHome: true,
      isPlaying: false,
      exitHome: false,
      delay: null,
      score: null,
      showResults: false,
      isDissolving: false,
      totalScore: 0,
      highscore: 0,
      counterStatus: false,
      levelVar: 5
    }
  },
  methods: {
    startCounter() {
      this.counterStatus = true
      console.log(this.levelVar);
    },
    calculateTotalScore() {
      this.totalScore += this.score
      this.levelVar *= 0.9
      document.querySelector(':root').style.setProperty('--speed', this.levelVar)
    },
    start()  {
      this.delay = 2000 + Math.random() * 5000
      this.exitHome = true
      setTimeout(() => { this.atHome = false }, 1500);
      this.isPlaying = true
      this.showResults = false
      this.isDissolving = false
      this.counterStatus = false
    },
    stopGame(reactionTime) {
      console.log(reactionTime);
      if (reactionTime*this.levelVar < 201) {this.score = 50}
        else if (reactionTime*this.levelVar <401) {this.score = 40}
        else if (reactionTime*this.levelVar <601) {this.score = 30}
        else if (reactionTime*this.levelVar <801) {this.score = 20}
        else {this.score = 10}
      setTimeout(() => {this.isPlaying = false}, 500);
      this.showResults = true
      this.calculateTotalScore()
    },
    dissolveProtester() {
      this.isDissolving = true
    },
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Averia+Libre:wght@400;700&display=swap');

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  height: 100vh;
  width: 100vw;
}

#app {
  font-family: 'Averia Libre', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000000;
  display: flex;
  align-items: stretch;
  justify-content: center;
  height: 100%;
  width: 100%;
}
.game {
  height: 100%;
  width: 100%;
  max-height: 1000px;
  max-width: 500px;
  position: relative;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  padding: 0 20px;
  background: lightgray;
}
.main-content {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  z-index: 1;
  perspective: 400px;
}
.background-content {
  z-index: 0;
}
button {
  font-family: 'Averia Libre', cursive;
  opacity: 1;
}
button.start, .points {
  background: #FF7A00;
  color: #E4DFDA;
  padding: 12px 20px;
  border: 3px solid #000000;
  box-shadow: 0px 4px 0px #000000;
  border-radius: 10px;
  font-size: 40px;
  font-weight: bold;
  text-shadow: 1px 0 0 #000000, -1px 0 0 #000000, 0 1px 0 #000000, 0 -1px 0 #000000, 2px 2px 0 #000000;
  margin: auto 0 120px 0;
  position: relative;
  z-index: 2;
  transition: 0.2s cubic-bezier(0.36, 0, 0.66, -0.56);
  transition-property: opacity, transform;
}
button[disabled] {
  opacity: 0;
  transform: scale(0.8)
             translateY(56px);
  cursor: not-allowed;
}
.game-title {
  margin-top: 26px;
  font-weight: bold;
  font-size: 48px;
  text-align: center;
  text-shadow: 1px 0 0 #000000, -1px 0 0 #000000, 0 1px 0 #000000, 0 -1px 0 #000000, 2px 2px 0 #000000;
  color: #FF7A00;
}
</style>
