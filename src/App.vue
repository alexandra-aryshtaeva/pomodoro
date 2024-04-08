<script setup>
import { ref } from "vue";
import Pomodoro from "./components/Pomodoro.vue";
// dont forget to update the localStorage
import ShortBreak from "./components/ShortBreak.vue";
import LongBreak from "./components/LongBreak.vue";

const currentTab = ref("pomodoro");
</script>
<template>
  <div class="card">
    <div id="topButtons">
      <button @click="currentTab = 'pomodoro'">Pomodoro</button>
      <button @click="currentTab = 'shortBreak'">Short Break</button>
      <button @click="currentTab = 'longBreak'">Long Break</button>
    </div>

    <Pomodoro v-if="currentTab === 'pomodoro'" />
    <ShortBreak v-if="currentTab === 'shortBreak'" />
    <LongBreak v-if="currentTab === 'longBreak'" />
  </div>
</template>

<style>
body {
  margin: 0px;
  padding: 0px;
  background-image: url(./assets/paper.png);
  background-size: cover;
  height: 100vh;
  width: 100vw;
  width: 100vw;
  background-position: center;
  font-size: 32px;
  display: flex;
  justify-content: center;
  text-align: center;
  align-items: center;
}

.card {
  display: flex;
  flex-direction: column;
  align-self: center;
  justify-self: center;
  padding: 0px;
  margin: 0px;
}

#display {
  margin: 4px 0px;
}
button {
  padding: 8px 8px;
  margin: 4px 16px;
}
</style>
