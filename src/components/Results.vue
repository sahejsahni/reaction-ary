<template>
  <div class="results">
    <p v-if="ongoing" class="points">+{{score}} Points</p>
    <p v-if="!ongoing" class="points">Your Score: {{totalScore}}</p>
  </div>
</template>

<script>
export default {
  props: ['score', 'totalScore','ongoing']
}
</script>

<style>
.results {
  margin-top: 48px;
}
p.points {
  font-size: 28px;
  padding: 10px 20px;
  display: inline-block;
  border: 2px solid #000000;
  box-shadow: 0px 2px 0px #000000;
  text-shadow: 0.7px 0 0 #000000, -0.7px 0 0 #000000, 0 0.7px 0 #000000, 0 -0.7px 0 #000000, 1.4px 1.4px 0 #000000;
  animation: pop-up 0.2s cubic-bezier(0.36, 0, 0.66, -0.56);
}
@keyframes pop-up {
  0% {
    opacity: 0;
    transform: scale(0.8)
              translateY(40px);
  }
  100% {
    opacity: 1;
    transform: scale(1)
              translateY(0);
  }
}
</style>