<template>
  <div class="results">
    <p class="points">+{{score}} Points</p>
  </div>
</template>

<script>
export default {
  props: ['score'],
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
}
</style>