<template>
  <div class="protester" v-if="showProtester" @click="stopTimer">
    <div class="slogan-wrapper">
      <p class="slogan">Hindu Khatre Mein Hai</p>
    </div>
    <img src="../assets/banner.png" alt="protester holding placard">
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showProtester:false,
      timer: null,
      reactionTime: 0
    }
  },
  mounted() {
    setTimeout(() => {
      this.showProtester = true
      this.startTimer()
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10
      }, 10)
    },
    stopTimer() {
      clearInterval(this.timer)
      this.$emit('end', this.reactionTime)
    }
  }
}
</script>

<style>

/* protester styles */
.protester {
  height: 640px;
  width: auto;
}
.protester.home {
  transform: rotate(36deg);
  position: absolute;
  bottom: -96px;
  left: -20px;
  transition: left 0.2s ease-in;
}
.protester.hide {
  left: -500px;
}
.protester img {
  height: 100%;
  width: auto;
}
.protester .slogan-wrapper {
  position: absolute;
  top: 1%;
  left: 6%;
  width: 85%;
  height: 41%;
  transform: rotate(-1.57deg);
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.protester .slogan {
  font-size: 36px;
  line-height: 40px;
  font-weight: bold;
  color: #38332E;
  margin-bottom: 20px;
  mix-blend-mode: multiply;
}


</style>