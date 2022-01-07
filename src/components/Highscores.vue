<template>
<div class="scores">
  <div class="highscore-container">
    <p>HIGH SCORE</p>
    <p class="highscore">{{highScore}}</p>
  </div>
  <div class="score-container">
    <p>SCORE</p>
    <p class="score">{{totalScore}}</p>
  </div>
</div>
</template>

<script>
export default {
  props: ['totalScore', 'highScore'],
  }
</script>

<style>
.highscore-container {
  display: flex;
  justify-content: space-between;
  padding: 20px 20px 12px 20px;
  margin: 0 -20px;
  font-size: 24px;
  background-color: #8A8A8A;
  border-bottom: 2px solid #000000;
  transition-property: background-color, box-shadow, border;
  transition: 1s ease-in-out;
  position: relative;
  z-index: 2;
}
.highscore {
  font-size: 27px;
  line-height: 24px;
  font-weight: bold;
  color: #FF7A00;
  text-shadow: 1px 0 0 #000000, -1px 0 0 #000000, 0 1px 0 #000000, 0 -1px 0 #000000, 1.5px 1.5px 0 #000000;
}
.scores.new-highscore .highscore-container{
  background-color: #FF7A00;
  box-shadow: 0px 4px 23px #FF9100;
  border-bottom: 2px solid #FEC880;
}
.scores.new-highscore .highscore{
  color: #f4ebe3;
}
.score-container {
  display: flex;
  justify-content: space-between;
  padding: 8px 20px 4px 20px;
  margin: 0 -20px;
  font-size: 24px;
  background-color: #c1b8ae;
  position: relative;
  z-index: 1;
}
</style>