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
      this.$emit('timerOn')
    }, this.delay);
  },
  methods: {
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
.dummy.game-over {
  position: absolute;
  display: inline-block;
  bottom: 0px;
  left: 0px;
  mix-blend-mode: normal;
  opacity: 0;
  animation: pop 400ms cubic-bezier(0.36, 0, 0.66, -0.56) forwards;
}
@keyframes pop {
  0% {
    opacity: 0;
    transform: scale(20%);
  }
  100% {
    opacity: 1;
    transform: scale(var(--d-scale));
  }
}
.dummy.one {
  --d-scale: 75%;
  transform: scale(var(--d-scale));
  left: 2%;
  transform-origin: bottom left;
  z-index: 1;
}
.dummy.two {
  --d-scale: 70%;
  transform: scale(var(--d-scale));
  animation-delay: 200ms;
  left: auto;
  right: 0;
  transform-origin: bottom right;
  z-index: 2;
}
.dummy.three {
  --d-scale: 60%;
  transform: scale(var(--d-scale));
  animation-delay: 400ms;
  left: auto;
  right: 0;
  transform-origin: 65% bottom;
  z-index: 3;
}
.dummy.four {
  --d-scale: 45%;
  transform: scale(var(--d-scale));
  animation-delay: 600ms;
  left: auto;
  right: 0;
  transform-origin: 90% 100%;
  z-index: 4;
}
.dummy.five {
  --d-scale: 35%;
  transform: scale(var(--d-scale));
  animation-delay: 800ms;
  transform-origin: 25% 100%;
  z-index: 5;
}
</style>