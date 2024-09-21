<template>
  <div class="timer-container">
    <div class="input-container">
      <div class="input-group">
        <label for="hours">Horas:</label>
        <input type="number" v-model="hours" min="0" max="23" :disabled="isRunning">
      </div>
      <div class="input-group">
        <label for="minutes">Minutos:</label>
        <input type="number" v-model="minutes" min="0" max="59" :disabled="isRunning">
      </div>
      <div class="input-group">
        <label for="seconds">Segundos:</label>
        <input type="number" v-model="seconds" min="0" max="59" :disabled="isRunning">
      </div>
    </div>
    <button id="startButton" @click="startTimer" :disabled="isRunning">Start</button>
    <div class="timer-display">
      {{ displayTime }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'TimerComponent',
  data() {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
      totalTimeInSeconds: 0,
      interval: null,
      isRunning: false
    };
  },
  computed: {
    displayTime() {
      const hrs = Math.floor(this.totalTimeInSeconds / 3600);
      const mins = Math.floor((this.totalTimeInSeconds % 3600) / 60);
      const secs = this.totalTimeInSeconds % 60;
      return `${this.pad(hrs)}:${this.pad(mins)}:${this.pad(secs)}`;
    }
  },
  methods: {
    startTimer() {
      this.totalTimeInSeconds = (this.hours * 3600) + (this.minutes * 60) + this.seconds;
      if (this.totalTimeInSeconds <= 0) {
        return;
      }
      
      this.isRunning = true;
      this.interval = setInterval(() => {
        if (this.totalTimeInSeconds <= 0) {
          clearInterval(this.interval);
          this.isRunning = false;
          return;
        }
        this.totalTimeInSeconds--;
      }, 1000);
    },
    pad(num) {
      return num < 10 ? '0' + num : num;
    }
  }
};
</script>

<style scoped>
@import '../assets/style.css';
</style>
