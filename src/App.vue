<script setup>
import { ref } from "vue";
const timer = ref(4);
let timeInterval;

function start() {
  if (timeInterval) return;

  timeInterval = setInterval(() => {
    timer.value--;

    if (timer.value === 0) {
      stop();
    }
  }, 1000);
}

function stop() {
  clearInterval(timeInterval);
}
</script>
<template>
  <button>Pomodoro</button>
  <button>Long Break</button>
  <button>Short Break</button>
  <div>{{ timer }}</div>
  <button @click="start">Start</button>
  <button @click="stop">Pause</button>
  <button>Restart</button>
  <button>Config</button>
</template>

<style>
body {
  font-size: 32px;
}
</style>
