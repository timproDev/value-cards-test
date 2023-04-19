<template>
    <div class="timer">
      <div class="progress-container">
        <div class="progress" :style="`width: ${progress}%`"></div>
      </div>
      <div class="countdown">{{ time }}</div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        time: 5,
        progress: 0
      };
    },
    props: [
      'cardsViewed'
    ],
    watch: { // watch data for changes
      cardsViewed() {
        console.log('card viewed') //if card this.cardsViewed, restart timer
      }
      // how to kill the timer and restart the timer if the varViewed data changes
    },
    emits: [
      'times-up'
    ],
    mounted() {
      this.startCountdown();
    },
    methods: {
      startCountdown() {
        let duration = this.time;
        let start = Date.now();
        let end = start + duration * 1000;
        
        let timer = setInterval(() => {
          let now = Date.now();
          let timeLeft = Math.round((end - now) / 1000);
  
          if (timeLeft < 0) {
            clearInterval(timer);
            this.progress = 100;
            this.$emit('times-up')
            return;
          }
  
          this.time = timeLeft;
          let elapsed = now - start;
          this.progress = (elapsed / (duration * 1000)) * 105;
        }, 50);
      }
    }
  };
  </script>
  
  <style scoped>
  .timer {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* height: 100vh; */
    /* position: absolute;
    top: -100px;
    left: 0;
    right: 0;
    margin: 0 auto; */
  }
  
  .progress-container {
    width: 80%;
    height: 10px;
    background-color: #ddd;
    border-radius: 5px;
    overflow: hidden;
  }
  
  .progress {
    height: 100%;
    background-color: #0077ff;
    transition: width 0.05s linear;
  }
  .countdown {
    margin-top: 10px;
    font-size: 2em;
  }
  </style>
  