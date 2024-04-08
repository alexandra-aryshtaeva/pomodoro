<script setup>
import { computed, ref, watch } from "vue";

//
const timer = ref(25 * 60);
// restart Only
const initalTimer = ref(25 * 60);
//
let timeInterval;
let startBtn = ref(true);
let input = ref("");

let showInput = ref(false);

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
    }
  }, 1000);
}

function stop() {
  startBtn.value = true;
  clearInterval(timeInterval);
  timeInterval = undefined;
}

function restart() {
  timer.value = initalTimer.value;
  stop();
}

// watch (source, (newValue,(function)=>{}), (optional: ){} )
// watch (input value, (function)=>{})

// will change the value of the config input and then is multiplied by 60 to convert to minutes
watch(input, (newInputValue) => {
  // input = newInputValue (minutes(ex:25))
  // newInputValue
  if (newInputValue >= 24 * 60) {
    newInputValue = 24 * 60;
  }
  if (newInputValue < 0) {
    newInputValue = 0;
  }

  timer.value = newInputValue * 60;
  //  minutes result

  // newInpouteValue => timer.value
});

function isInput() {
  showInput.value = true;
}
</script>

<template>
  <div id="display">{{ display }}</div>
  <button v-if="startBtn" @click="start">Start</button>
  <button v-if="!startBtn" @click="stop">Pause</button>
  <button @click="restart">Restart</button>
  <button @click="isInput">Config</button>
  <input v-if="showInput" type="number" v-model="input" />
</template>
