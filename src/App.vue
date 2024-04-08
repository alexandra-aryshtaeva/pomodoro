<script setup>
import { ref } from "vue";
import Pomodoro from "./components/Pomodoro.vue";
// dont forget to update the localStorage
import ShortBreak from "./components/ShortBreak.vue";
import LongBreak from "./components/LongBreak.vue";

const currentTab = ref("pomodoro");
</script>
<template>
  <button @click="currentTab = 'pomodoro'">Pomodoro</button>
  <button @click="currentTab = 'shortBreak'">Short Break</button>
  <button @click="currentTab = 'longBreak'">Long Break</button>

  <Pomodoro v-if="currentTab === 'pomodoro'" />
  <ShortBreak v-if="currentTab === 'shortBreak'" />
  <LongBreak v-if="currentTab === 'longBreak'" />
</template>

<style>
body {
  font-size: 32px;
}
</style>

<!-- <script setup>
import { ref, onMounted } from 'vue'
import Child from './Child.vue'

const child = ref(null)

onMounted(() => {
  // child.value will hold an instance of <Child />
})
</script>

<template>
  <Child ref="child" />
</template> -->
