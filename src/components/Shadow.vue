<template>
  <div class="shadow-wrapper">
    <img src="../assets/shadow.png" alt="" class="shadow">
  </div>
</template>

<script>
export default {

}
</script>

<style>
.shadow-wrapper {
  height: 65vh;
  max-height: 640px;
  position: absolute;
  width: 90vw;
  max-width: 400px;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  z-index: -2;
}
.shadow {
  height: 100%;
  width: auto;
  animation: shadow-appear 0.5s;
}
@keyframes shadow-appear {
  0%   {
    opacity: 0;
    }
  100% {
    opacity: 1;
  }
}
</style>