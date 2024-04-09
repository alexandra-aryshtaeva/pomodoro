<script setup>
import { ref } from "vue";
import Pomodoro from "./components/Pomodoro.vue";
// dont forget to update the localStorage
import ShortBreak from "./components/ShortBreak.vue";
import LongBreak from "./components/LongBreak.vue";

const currentTab = ref("pomodoro");
</script>

<template>
  <main>
    <div class="card">
      <div id="tab-buttons">
        <button @click="currentTab = 'pomodoro'">Pomodoro</button>
        <button @click="currentTab = 'shortBreak'">Short Break</button>
        <button @click="currentTab = 'longBreak'">Long Break</button>
      </div>

      <Pomodoro v-if="currentTab === 'pomodoro'" />
      <ShortBreak v-if="currentTab === 'shortBreak'" />
      <LongBreak v-if="currentTab === 'longBreak'" />
    </div>
  </main>
</template>

<style>
html {
  height: 100vh;
  --pink: #ed8f83;
}

body {
  margin: 0px;
  padding: 0px;
  background-image: url(./assets/paper.png);
  background-size: cover;
  background-position: center;
  height: 100%;
}

/* vue own div (click on inspect its under body) */
#app {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
}

main {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.card {
  display: flex;
  flex-direction: column;

  align-items: center;
  flex: 1;
  height: 100%;
  width: 100%;
}

.display {
  font-family: "Indie Flower";
  font-size: 128px;
  font-weight: 600;
  display: flex;
  flex: 3;
  align-items: center;
  transform: rotate(7deg);
  color: var(--pink);
  text-shadow: 3px 0px 3px rgb(165, 115, 115);
}

.display.active {
  animation: timer infinite 1s;
}

@keyframes timer {
  0% {
    transform: rotate(5deg);
  }
  50% {
    transform: rotate(-5deg);
  }
  100% {
    transform: rotate(5deg);
  }
}

@media screen and (min-width: 768px) {
  .display {
    font-size: 160px;
  }
}

#tab-buttons {
  /* background-color: antiquewhite; */
  display: flex;
  align-items: center;
  flex: 1;
  gap: 12px;
}

@media screen and (min-width: 768px) {
  #tab-buttons {
    gap: 32px;
  }
}

.menu {
  /* background-color: aqua; */
  display: flex;
  flex: 1;
  align-items: center;
  gap: 12px;

  button {
    padding: 8px 32px;
  }
}

@media screen and (min-width: 768px) {
  .menu {
    gap: 32px;
  }
}

button {
  cursor: pointer;
  padding: 8px 16px;
  margin: 0px 0px;
  font-family: "Indie Flower";
  font-weight: 600;
  font-size: 16px;
  color: var(--pink);
  background-color: #aa4a3e;
  border-radius: 16px;
  border: solid var(--pink) 4px;
}

button:hover {
  background-color: white;
  color: #88392e;
  box-shadow: 0px 4px 8px #88392e;
  transform: translateY(-4px);
}

@media screen and (min-width: 768px) {
  button {
    font-size: 32px;
  }
}
</style>
