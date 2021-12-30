<template>
  <div class="results">
    <p>Reaction Time {{score}} ms</p>
    <p class="rank">{{rank}}</p>
  </div>
</template>

<script>
export default {
  props: ['score'],
  data() {
    return {
      rank: null
    }
  },
  mounted() {
    if (this.score < 250) {
      this.rank = 'Ninja Fingers'
    } else if (this.score < 400) {
      this.rank = 'Rapid Reflexes'
    } else {
      this.rank = 'Snail pace...'
    }
  }
}
</script>

<style>
.results {
  position: absolute;
  width: 100%;
  height: 100%;
}
.rank {
  margin-top: 160px;
  font-size: 1.4em;
  color: #0faf87;
  font-weight: bold;
}
</style>