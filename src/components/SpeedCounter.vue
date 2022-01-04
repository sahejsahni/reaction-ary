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
  --speed: 1;
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
  border-radius: 50px;
  border: 2px solid #38332E;
  overflow: hidden;
  position: relative;
  background-color: #E4DFDA;
  margin: 0;
}
.blip {
  position: relative;
  margin: 0px;
  height: 10px;
  background-color: red;
  transform: translateX(-110%);
  animation: none;
}
.speed-counter.animate .blip {
  animation: fill-blip linear forwards;
  animation-duration: calc(var(--speed)*5s);
}
.speed-counter.pause .blip {
  animation-play-state: paused;
}
.blip.first {
  background-color: #12B76A;
  left: -280px;
  width: 280px;
}
.blip.second {
  background-color: #FFD663;
  left: -272px;
  width: 224px;
}
.blip.third {
  background-color: #FDB022;
  left: -264px;
  width: 168px;
}
.blip.fourth {
  background-color: #F79009;
  left: -256px;
  width: 112px;
}
.blip.fifth {
  background-color: #F04438;
  left: -248px;
  width: 56px;
}
@keyframes fill-blip {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(236px);
  }
}
</style>