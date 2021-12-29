<template>
  <div class="game">
    <div class="main-content">
      <!-- high score -->
      <div class="highscore-container">
        <p>HIGH SCORE</p>
        <p class="highscore">320</p>
      </div>

      <div class="heading-container">
        <h1 class="game-title">Reaction-ary</h1>
      </div>

      <!-- instructions -->
      <div class="instructions">
        <h2>Instructions</h2>
        <ol>
          <li>Smash the reactionary as soon as you see him.</li>
          <li>Difficulty increases as you advance, so gear up.</li>
        </ol>
      </div>

      <button class="start" @click="start" :disabled="isPlaying">Start</button>
    </div>

    <div class="background-content">
      <Protester v-if="atHome" class="home" :class="{ 'hide': exitHome }"/>
    </div>

    <Protester v-if="isPlaying" class="playing" :delay="delay" @end="endGame" />
    <Results v-if="showResults" :score="score" />
  </div>
</template>

<script>
import Protester from './components/Protester.vue'
import Results from './components/Results.vue'
export default {
  name: 'App',
  components: { Protester, Results },
  data() {
    return {
      atHome: true,
      isPlaying: false,
      exitHome: false,
      delay: null,
      score: null,
      showResults: false
    }
  },
  methods: {
    start()  {
      this.delay = 2000 + Math.random() * 5000
      this.exitHome = true
      setTimeout(() => {
        this.atHome = false
        console.log(atHome);
      }, 1000);
      this.isPlaying = true
      this.showResults = false
    },
    endGame(reactionTime) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
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
  max-height: 840px;
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
}
.background-content {
  z-index: 0;
}

/* highscore styles */
.highscore-container {
  display: flex;
  justify-content: space-between;
  padding: 20px 20px 12px 20px;
  margin: 0 -20px;
  font-size: 24px;
  background-color: #DACDBF;
  border-bottom: 2px solid #000000;
}
.highscore {
  font-weight: bold;
  color: #FF7A00;
  text-shadow: 1px 0 0 #000000, -1px 0 0 #000000, 0 1px 0 #000000, 0 -1px 0 #000000, 1.5px 1.5px 0 #000000;
}

button {
  font-family: 'Averia Libre', cursive;
}
button.start {
  background: #FF7A00;
  color: #E4DFDA;
  padding: 12px 20px;
  border: 3px solid #000000;
  box-sizing: border-box;
  box-shadow: 0px 4px 0px #000000;
  border-radius: 10px;
  font-size: 40px;
  font-weight: bold;
  text-shadow: 1px 0 0 #000000, -1px 0 0 #000000, 0 1px 0 #000000, 0 -1px 0 #000000, 2px 2px 0 #000000;
  margin: auto 0 120px 0;
  position: relative;
  z-index: 2;
}
button[disabled] {
  opacity: 0.2;
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
/* instructions styles */
.instructions h2 {
  text-decoration: underline;
  font-size: 28px;
  margin: 20px 0;
}
.instructions ol{
  list-style-type: decimal;
  text-align: left;
  list-style-position: inside;
  display: inline-block;
}
</style>
