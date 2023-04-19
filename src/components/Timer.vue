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
      }
    },
    emits: [
      'times-up'
    ],
    mounted() {
      this.timerFunc();
    },
    methods: {
      timerFunc() {
        let duration = this.time;
        let start = Date.now();
        let end = start + duration * 1000;        
        
        let timerTest = setInterval(() => {
          let now = Date.now();
          let timeLeft = Math.round((end - now) / 1000);          

          this.time = timeLeft;
          let elapsed = now - start;
          this.progress = (elapsed / (duration * 1000)) * 100;

          if (timeLeft < 0) {
          // if (timeLeft < 0 || this.timerStatus == false) {
            clearInterval(timerTest);
            this.progress = 0;
            this.time = 5;
            this.$emit('times-up')
            return;
          } else if (this.timeStopped) {
            clearInterval(timerTest);
            this.progress = 0;
            this.time = 5;
          }
        }, 5);
        // https://stackoverflow.com/questions/8126466/how-do-i-reset-the-setinterval-timer
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
  