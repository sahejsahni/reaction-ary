<template>
  <div class="speed-counter">
    <div class="blip-wrapper">
      <div class="blip first"></div>
    </div>
    <div class="blip-wrapper">
      <div class="blip second"></div>
    </div>
    <div class="blip-wrapper">
      <div class="blip third"></div>
    </div>
    <div class="blip-wrapper">
      <div class="blip fourth"></div>
    </div>
    <div class="blip-wrapper">
      <div class="blip fifth"></div>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>
:root {
  --speed: 3;
}
.speed-counter {
  display: flex;
  flex-direction: row;
  width: 280px;
  margin: 32px auto 0 auto;
}
.blip-wrapper {
  height: 10px;
  width: 48px;
  margin: 0 5px;
  border-radius: 50px;
  border: 2px solid #38332E;
  overflow: hidden;
  position: relative;
  background-color: #f4ebe3;
}
.blip {
  position: relative;
  margin: -2px;
  height: 10px;
  width: 48px;
  background-color: red;
  transform: translateX(-100%);
}
.speed-counter.animate .blip {
  animation: fill-blip linear forwards;
  animation-duration: calc(var(--speed)*200ms);
}
.speed-counter.pause .blip {
  animation-play-state: paused;
}
.speed-counter .blip.first {
  background-color: #12B76A;
  animation-delay: calc(var(--speed)*0);
}
.speed-counter .blip.second {
  background-color: #FFD663;
  animation-delay:  calc(var(--speed)*200ms);
}
.speed-counter .blip.third {
  background-color: #FDB022;
  animation-delay:  calc(var(--speed)*400ms);
}
.speed-counter .blip.fourth {
  background-color: #F79009;
  animation-delay:  calc(var(--speed)*600ms);
}
.speed-counter .blip.fifth {
  background-color: #F04438;
  animation-delay:  calc(var(--speed)*800ms);
}
@keyframes fill-blip {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(0);
  }
}
</style>