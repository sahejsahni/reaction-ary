<template>
  <div class="shadow-wrapper">
    <img src="../assets/shadow(1).png" alt="" class="shadow">
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
  filter: blur(4px);
  animation: shadow-appear 0.5s ease-out;
  mix-blend-mode: darken;
}
@keyframes shadow-appear {
  0%   {
    opacity: 0;
    filter: blur(20px);
    }
  100% {
    opacity: 1;
    filter: blur(4px);
  }
}
</style>