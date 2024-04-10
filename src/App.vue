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

/*__________________ DISPLAY */

.display-wrapper {
  position: relative;
  height: 300px;
}

@media screen and (min-width: 768px) {
  .display-wrapper {
    font-size: 260px;
    height: 450px;
  }
}

.display {
  font-family: "Indie Flower";
  font-size: 112px;
  font-weight: 600;
  display: flex;
  flex: 3;
  align-items: center;
  position: absolute;
  top: 25%;
  left: 13%;
  transform: rotate(5deg);
  color: var(--pink);
  text-shadow: 3px 0px 3px rgb(90, 54, 54);
}

.display.active {
  animation: timer infinite 1s;
}

@keyframes timer {
  0% {
    transform: rotate(5deg);
  }
  50% {
    transform: rotate(-3deg);
  }
  100% {
    transform: rotate(5deg);
  }
}

@media screen and (min-width: 768px) {
  .display {
    font-size: 168px;
    transform: rotate(5deg);
  }
}

.tomato {
  opacity: 0.8;
  height: 300px;
  transform: rotate(-5deg);

  -webkit-filter: drop-shadow(0px 0px 5px #222);
  filter: drop-shadow(0px 0px 5px #222);
}

.tomato.active {
  animation: sticker infinite 1s;
}

@keyframes sticker {
  0% {
    transform: rotate(-2deg);
  }
  50% {
    transform: rotate(2deg);
  }
  100% {
    transform: rotate(-2deg);
  }
}

@media screen and (min-width: 768px) {
  .tomato {
    height: 450px;
  }
}

/*________________________ BUTTONS */

#tab-buttons {
  /* background-color: antiquewhite; */
  display: flex;
  align-items: center;
  flex: 1;
  gap: 4px;
  margin-bottom: 110px;
}

@media screen and (min-width: 768px) {
  #tab-buttons {
    margin-bottom: 200px;
    gap: 32px;
  }
}

.menu {
  /* background-color: aqua; */
  display: flex;
  flex: 1;
  align-items: center;
  gap: 4px;
  margin-top: 110px;

  button {
    padding: 8px 32px;
  }
}

@media screen and (min-width: 768px) {
  .menu {
    margin-top: 200px;
    gap: 32px;
  }
}

button {
  cursor: pointer;
  padding: 8px 16px;
  margin: 0px 0px;
  font-family: "Indie Flower";
  font-weight: 800;
  font-size: 18px;
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

.modal {
  display: block;
  align-content: center;

  position: absolute;
  height: 100vh;
  width: 100vw;
  background-color: rgba(126, 126, 126, 0.5);
}
#input {
  display: block;
  margin: 0 auto;
  height: 40px;
  width: 100px;
  color: white;
  background-color: #88392e;
  outline: none;
  border: solid white 2px;
  border-radius: 8px;
  padding-left: 8px;
  text-align: center;
  font-size: 20px;
}
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
}
@media screen and (min-width: 768px) {
  #input {
    font-size: 20px;
    height: 40px;
    width: 350px;
  }
}
</style>
