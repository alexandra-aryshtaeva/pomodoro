<script setup>
import { computed, ref, watch } from "vue";

const INITIAL_MINUTES = 15;
const DEFAULT_MINUTES = Number(
  localStorage.getItem("longBreaktimer") ?? INITIAL_MINUTES
);

const timer = ref(DEFAULT_MINUTES * 60);
// restart Only
const initalTimer = INITIAL_MINUTES * 60;

let timeInterval;
let startBtn = ref(true);
let input = ref(DEFAULT_MINUTES);
let showInput = ref(false);
let audio = new Audio("/ding.wav");
let modal = ref(false);

const display = computed(() => {
  let minutes = Math.floor(timer.value / 60);
  let seconds = Math.round((timer.value / 60 - minutes) * 60);
  if (minutes < 10) {
    minutes = "0" + minutes;
  }
  if (seconds < 10) {
    seconds = "0" + seconds;
  }
  return minutes + ":" + seconds;
});

function start() {
  if (timeInterval) return;
  startBtn.value = false;

  timeInterval = setInterval(() => {
    timer.value--;

    if (timer.value === 0) {
      stop();
      audio.play();
    }
  }, 1000);
}

function stop() {
  startBtn.value = true;
  clearInterval(timeInterval);
  timeInterval = undefined;
}

function restart() {
  timer.value = initalTimer;
  localStorage.setItem("longBreaktimer", INITIAL_MINUTES);
  stop();
}

// watch (source, (newValue,(function)=>{}), (optional: ){} )
// watch (input value, (function)=>{})

// will change the value of the config input and then is multiplied by 60 to convert to minutes
watch(input, (newInputValue) => {
  // input = newInputValue (minutes(ex:25))
  // newInputValue
  if (newInputValue >= 99) {
    newInputValue = 99;
    input.value = newInputValue;
  }
  if (newInputValue < 0) {
    newInputValue = 0;
  }

  // minutes result
  timer.value = newInputValue * 60;

  localStorage.setItem("longBreaktimer", newInputValue);
});

function showModal() {
  modal.value = true;
  showInput.value = true;
}
</script>

<template>
  <div class="display-wrapper">
    <img class="tomato" src="/tomato.png" alt="" />
    <div class="display" :class="{ active: !startBtn }">{{ display }}</div>
  </div>

  <div class="menu">
    <button v-if="startBtn" @click="start">Start</button>
    <button v-if="!startBtn" @click="stop">Pause</button>
    <button @click="restart">Restart</button>
    <button @click="showModal">Config</button>
  </div>
  <div v-if="modal" ref="modal" class="modal">
    <input
      @keyup.enter="modal = false"
      id="input"
      type="number"
      v-model="input"
    />
  </div>
</template>
