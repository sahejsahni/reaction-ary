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
  display: inline-block;
  height: 65vh;
  max-height: 640px;
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
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