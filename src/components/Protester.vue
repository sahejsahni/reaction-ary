<template>
  <div class="protester" v-if="showProtester" @click="stopTimer">
    <div class="slogan-wrapper">
      <p class="slogan">
        {{slogan}}
      </p>
    </div>
    <img src="../assets/protester.png" alt="protester holding placard">
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showProtester:false,
      timer: null,
      reactionTime: 0,
      slogan: null

    }
  },
  mounted() {
    setTimeout(() => {
      this.sourceSlogan()
      this.showProtester = true
      this.startTimer()
      this.$emit('timerOn')
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
      this.$emit('stop', this.reactionTime)
    },
    sourceSlogan() {
      var collection = [
        "Hindu Khatre Mein Hai",
        "Not All Men",
        "Freedom Over Safety",
        "Vaccines Cause Autism",
        "I Fear God Not Covid"
        ]
      this.slogan = collection[Math.floor(Math.random()*collection.length)];
    }
  }
}
</script>

<style>

/* protester styles */
.protester {
  height: 640px;
  width: auto;
  mix-blend-mode: darken;
}
.protester.home {
  transform: rotate(36deg);
  position: absolute;
  bottom: -96px;
  left: -20px;
  transition: 0.4s cubic-bezier(0.36, 0, 0.66, -0.56) 0.5s;
  transition-property: left, transform;
}
.protester.hide {
  left: -500px;
  transform: rotate(12deg);
}
.protester img {
  height: 100%;
  width: auto;
}
.protester .slogan-wrapper {
  position: absolute;
  top: 1%;
  left: 7%;
  width: 85%;
  height: 41%;
  transform: rotate(-1.57deg);
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.protester .slogan {
  font-size: 4.45544554vh;
  line-height: 4.95049505vh;
  font-weight: bold;
  color: #38332E;
  margin-bottom: 20px;
  mix-blend-mode: multiply;
}
.protester.playing {
  height: 65vh;
  max-height: 640px;
  position: absolute;
  width: 90vw;
  max-width: 400px;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
  z-index: -1;
  transform-origin: 50% 100%;
}
.protester.playing {
  animation: protester-appear 0.2s cubic-bezier(0.34, 1.2, 0.64, 1);
}
@keyframes protester-appear {
  0%   {
    transform: rotate3d(0.53, 0, 0, 90deg);
    }
  100% {
    transform: rotate3d(0, 0, 0, 0deg);
  }
}
.protester.playing.dissolving {
  transition: opacity 0.5s;
  opacity: 0;
}
</style>