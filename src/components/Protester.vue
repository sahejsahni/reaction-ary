<template>
  <div class="protester" v-if="showProtester" @click="stopTimer">
    <div class="slogan-wrapper">
      <p class="slogan">
        {{slogan}}
      </p>
    </div>
    <img src="../assets/protester(1).png" alt="protester holding placard">
  </div>
</template>

<script>
export default {
  props: ['delay', 'levelVar'],
  data() {
    return {
      showProtester: false,
      timer: null,
      reactionTime: 0,
      slogan: null,
      gameOver: false
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
      var t = this.levelVar * 1000
      this.timer = setInterval(() => {
        this.reactionTime += 10
        if (this.reactionTime > t) {
          this.endGame()
          }
      }, 10)
    },
    endGame() {
      clearInterval(this.timer)
      this.$emit('end')
      this.slogan = "The reactionaries have won 😩"
    },
    stopTimer() {
      if (!this.gameOver) {
        clearInterval(this.timer)
        this.$emit('stop', this.reactionTime)
      }
    },
    sourceSlogan() {
      var collection = [
        "Hindu Khatre Mein Hai",
        "Not All Men",
        "Freedom Over Safety",
        "Vaccines Cause Autism",
        "I Fear God Not Covid",
        "Ban Abortions"
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
  position: relative;
  display: inline-block;
  -webkit-tap-highlight-color: transparent;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.protester:focus {
  outline: none !important;
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
  left: 6%;
  width: 86%;
  height: 41%;
  z-index: 2;
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
  bottom: 0;
  margin: auto;
  transform-origin: 50% 100%;
  cursor: pointer;
}
.protester.playing {
  animation: protester-appear 200ms cubic-bezier(0.34, 1.2, 0.64, 1);
}
.protester.shake {
  animation: shake 2000ms linear;
}
@keyframes protester-appear {
  0%   {
    transform: rotate3d(0.53, 0, 0, 90deg);
    }
  100% {
    transform: rotate3d(0, 0, 0, 0deg);
  }
}
@keyframes shake {
  0% {
    transform: rotate3d(0.53, 0, 0, 0deg)  
  }
  1% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  2% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  3% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  4% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  5% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  6% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  7% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  8% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  9% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  10% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  11% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  12% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  13% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  14% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  15% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  16% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  17% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  18% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  19% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  20% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  21% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  22% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  23% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  24% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  25% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  26% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  27% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  28% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  29% {
    transform: rotate3d(0.53, 0, 0.02, 10deg);
    filter: brightness(90%); 
  }
  30% {
    transform: rotate3d(0.53, 0, -0.02, 10deg);
    filter: brightness(90%); 
  }
  50% {
    transform: rotate3d(0.53, 0, 0, 0deg)
  }
  100% {
    transform: rotate3d(0.53, 0, 0, 0deg)  
  }
}
.protester.playing.dissolving {
  transition-duration: 0.5s;
  transition-property: opacity, filter;
  opacity: 0;
  filter: blur(8px);
}
</style>