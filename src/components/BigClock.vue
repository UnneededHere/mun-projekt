<template>
  <div>
    <h1 :style="flashStyle">{{ minutes }}:{{ seconds }}</h1>
    <button @click="togglePlaying">{{ playingIcon }}</button>
    <button @click="nextSpeaker">Next Speaker</button>
  </div>
</template>
  
  <script>
export default {
  data() {
    return {
      time: this.startTime,
      isPlaying: false,
      timerInterval: null,
      flashInterval: null,
      isFlashing: false,
    };
  },
  props: {
    startTime: Number,
  },
  computed: {
    playingIcon() {
      return this.isPlaying ? "⏸" : "▶";
    },
    minutes() {
      const minutes = Math.floor(this.time / 60);

      return String(minutes).padStart(2, "0");
    },
    seconds() {
      const seconds = this.time % 60;

      return String(seconds).padStart(2, "0");
    },
    flashStyle() {
      return {
        color: this.isFlashing ? "red" : "black",
      };
    }
  },
  methods: {
    // Just something to note - since this only considers seconds, if a user pauses midway through a second and then resumes the countdown, the whole second has to pass before continuing.
    togglePlaying() {
      if (!this.isPlaying && this.time > 0) {
        this.isPlaying = true;
        this.timerInterval = setInterval(() => {
          this.time -= 1;
          if (this.time == 0) {
            clearInterval(this.timerInterval);
            this.startFlashing();
          }
        }, 1000);
      } else {
        this.isPlaying = false;
        clearInterval(this.timerInterval);
        this.stopFlashing();
      }
    },
    startFlashing() {
      this.isFlashing = true;
      this.flashInterval = setInterval(() => {
        this.isFlashing = !this.isFlashing;
      }, 1000);
    },
    stopFlashing() {
      clearInterval(this.flashInterval);
      this.isFlashing = false;
    },
    nextSpeaker() {
      this.stopFlashing();
      this.isPlaying = false;
      clearInterval(this.timerInterval);
      this.time = this.startTime;
      this.$emit('next-speaker');
    }
  },
};
</script>
  
  <style scoped>
    h1 {
      font-size: 100px;
      margin: 0;
    }
</style>
  