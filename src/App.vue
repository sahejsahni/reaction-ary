<template>
  <div class="game">
    <div class="main-content">
      <Highscores :totalScore="totalScore" :highScore="highScore" :class="{'new-highscore': newHighScore}"></Highscores>
      
      <div class="heading-container">
        <h1 class="game-title">Reaction-ary</h1>
      </div>
      
      <SpeedCounter :class="{ 'pause': isDissolving, 'animate': counterStatus }"></SpeedCounter>
      
      <Results v-if="showResults" :ongoing="ongoing" :score="score" :totalScore="totalScore" />
      
      <Instructions :class="{ 'hide': exitHome }"></Instructions>
      
      <div class="protester-wrapper">
        <div v-if="gameOver" class="avoid-click"></div>
        <Shadow v-if="isDissolving"></Shadow>
        <Protester v-if="isPlaying" class="playing" :class="[{ 'dissolving': isDissolving }, { 'shake': !ongoing }]" :levelVar="levelVar" :gameOver="gameOver" :delay="delay+200" @end="gameEnded" @stop="stopGame" @timerOn="startCounter"/>
      </div>
      
      <button v-if="gameOver" class="start" @click="resetGame" :class="{'pop': gameOver}">Restart</button>
      <button v-if="ongoing" class="start" @click="start" :class="[{'pop': !isPlaying}, {'remove': !showContinue}]">Continue</button>
      <button v-if="atHome" class="start" @click="start" :class="{'pop': !exitHome}">Start</button>
    </div>
    <div class="background-content">
      <Dummy v-if="atHome" class="home" :class="{ 'hide': exitHome }"/>
      <Dummy v-if="gameOver" class="dummy game-over one" />
      <Dummy v-if="gameOver" class="dummy game-over two" />
      <Dummy v-if="gameOver" class="dummy game-over three" />
      <Dummy v-if="gameOver" class="dummy game-over four" />
      <Dummy v-if="gameOver" class="dummy game-over five" />
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
import Dummy from './components/Dummy.vue'
export default {
  name: 'App',
  components: { Protester, Results, Instructions, Shadow, Highscores, SpeedCounter, Dummy },
  data() {
    return {
      atHome: true,
      isPlaying: false,
      ongoing: false,
      showContinue: false,
      exitHome: false,
      delay: null,
      score: null,
      showResults: false,
      isDissolving: false,
      totalScore: 0,
      highScore: 0,
      newHighScore: false,
      counterStatus: false,
      levelVar: 5,
      gameOver: false
    }
  },
  mounted() {
    if (localStorage.highScore) {
      this.highScore = localStorage.highScore
    }
  },
  methods: {
    startCounter() {
      this.counterStatus = true
    },
    calculateTotalScore() {
      this.totalScore += this.score
      this.levelVar *= 0.9
    },
    start()  {
      this.delay = 2000 + Math.random() * 5000
      this.exitHome = true
      setTimeout(() => { 
        this.atHome = false 
        this.ongoing = true
      }, 1500);
      this.isPlaying = true
      this.showContinue = false
      this.showResults = false
      this.isDissolving = false
      this.counterStatus = false
      this.gameOver= false
      document.querySelector(':root').style.setProperty('--speed', this.levelVar)
    },
    stopGame(reactionTime) {
      this.dissolveProtester()
      var e = 1 / this.levelVar
      var y = e * reactionTime
      if (y < 201) {this.score = 50}
        else if (y <401) {this.score = 40}
        else if (y <601) {this.score = 30}
        else if (y <801) {this.score = 20}
        else {this.score = 10}
      setTimeout(() => {
        this.isPlaying = false
        }, 500);
      this.showResults = true
      this.showContinue = true
      this.calculateTotalScore()
      if (this.totalScore > this.highScore) {
        this.highScore = this.totalScore
        this.newHighScore = true
        setTimeout(() => {
          this.newHighScore = false
        }, 1500);
      }
    },
    resetGame() {
      this.showResults = false
      this.dissolveProtester()
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = false
      this.totalScore = 0
      this.counterStatus = false
      this.atHome = true
      this.exithome = false
      this.gameOver = false
      setTimeout(() => {
        this.start()
      }, 500);
    },
    dissolveProtester() {
      if (!this.gameOver) {
        this.isDissolving = true
      }
    },
    gameEnded() {
      this.showResults = true
      this.ongoing = false
      this.gameOver = true
    }
  },
  watch: {
    highScore(newHighScore) {
      localStorage.highScore = newHighScore
    }
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
  background: #E4DFDA;
}
.main-content {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  z-index: 1;
  perspective: 400px;
}
.protester-wrapper {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 65vh;
  max-height: 640px;
}
.background-content {
  z-index: 0;
  width: 100%;
}
button {
  font-family: 'Averia Libre', cursive;
  opacity: 0;
  transform: scale(0.8)
             translateY(56px);
  cursor: pointer;
}
.remove {
  display: none;
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
  z-index: 20;
  transition: 0.2s cubic-bezier(0.36, 0, 0.66, -0.56);
  transition-property: opacity, transform;
}
button.pop {
  opacity: 1;
  transform: scale(1)
             translateY(0);
  cursor: pointer;
}
.game-title {
  margin-top: 26px;
  font-weight: bold;
  font-size: 48px;
  text-align: center;
  text-shadow: 1px 0 0 #000000, -1px 0 0 #000000, 0 1px 0 #000000, 0 -1px 0 #000000, 2px 2px 0 #000000;
  color: #FF7A00;
}
.avoid-click {
  background-color: grey;
  opacity: 0;
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 5;
}
</style>
