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
        time: 10,
        progress: 0
      };
    },
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
            return;
          }
  
          this.time = timeLeft;
  
          let elapsed = now - start;
          this.progress = (elapsed / (duration * 1000)) * 100;
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
    position: absolute;
    top: 120px;
    left: 0;
    right: 0;
    margin: 0 auto;
  }
  
  .progress-container {
    width: 80%;
    height: 20px;
    background-color: #ddd;
    border-radius: 10px;
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
  