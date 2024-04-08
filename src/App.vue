<script setup>
import Pomodoro from "./components/Pomodoro.vue";

// const current = ref(Pomodoro);
</script>
<template>
  <button>Long Break</button>
  <button>Short Break</button>
  <Pomodoro />
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
