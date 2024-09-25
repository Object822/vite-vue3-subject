<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import { ref } from "vue"
const countNum = ref('我是一个')
let childNum = ref(0)
console.log('countNum----->', countNum)
const changeData = (num: number) => {
  childNum.value = num
}
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" v-model:countData.trim="countNum" @changeChildNum="changeData">
    <template #header="headerProps">
      <span>我是头部{{ headerProps.torefData2 }}</span>
    </template>
    <span>我是默认的</span>
    <template #footer>
      <span>我是底部</span>
    </template>
  </HelloWorld>
  {{ childNum }}
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
