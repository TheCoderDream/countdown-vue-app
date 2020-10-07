<template>
  <div class="app">
    <h2>{{title}}</h2>

    <div class="timer">
      <span>{{minutes}}</span>
      <span>:</span>
      <span>{{seconds}}</span>
    </div>

    <div class="buttons">
      <button v-on:click="startTimer" v-if="!isRunning">Start</button>
      <button v-on:click="stopTimer" v-else>Stop</button>
      <button v-on:click="resetTimer">Reset</button>
    </div>
  </div>
</template>

<script>
function padTime(time) {
  return time.toString().padStart(2, '0');
}

export default {
  name: 'App',
  data() {
    return {
      title: 'Let the countdown begin!!',
      timeLeft: 15,
      isRunning: false,
      intervalId: null
    }
  },
  computed: {
    minutes() {
      return padTime(Math.floor(this.timeLeft / 60))
    },
    seconds() {
      return padTime(this.timeLeft - (this.minutes * 60));
    }
  },
  methods: {
    startTimer() {
      if (this.intervalId !== null) return;
      this.title = `You're doung great!`;
      this.isRunning = true;

      this.intervalId = setInterval(() => {
        if (this.timeLeft >= 1) return --this.timeLeft;
        this.timeLeft = 0;
      }, 1000);
    },
    stopTimer() {
      if (this.intervalId === null) return;
      clearInterval(this.intervalId);
      this.intervalId = null;
      this.isRunning = false;
    },
    resetTimer() {
      clearInterval(this.intervalId);
      this.intervalId = null;
      this.title = 'Ready to go another round?';
      this.timeLeft = 25*60;
      this.isRunning = false;
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Major+Mono+Display&display=swap');

* {
  box-sizing: border-box;
}

body {
  padding: 0;
  margin: 0;
  font-family: 'Major Mono Display', monospace;
  line-height: 1.5;
}

.app {
  min-height: 100vh;
  padding-left: 20px;
  padding-right: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: #87d7cc;
  color: #2c888d;
}

h2 {
  color: #49b2b8;
  font-size: 30px;
  text-align: center;
  margin: 0;
}

.timer {
  color: #1f6e72;
  font-size: 150px;
  margin-bottom: 20px;
}

.buttons button {
  outline: none;
  border: none;
  font-size: 24px;
  background: #f7fca0;
  color: #878b32;
  border-radius: 5px;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  padding: 15px 30px;
  cursor: pointer;
  transition: 0.3s ease all;
}

.buttons button:hover {
  border-radius: 10px;
  background: #f5f8ca;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.15);
  transform: translateY(-2px);
}

.buttons button:not(:last-child) {
  margin-right: 10px;
}

@media (max-width: 780px) {
  h2 {
    font-size: 22px;
  }

  .timer {
    font-size: 80px;
  }

  .buttons button {
    font-size: 18px;
  }
}
</style>
