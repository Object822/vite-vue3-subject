<!--
 * @Author: linhao
 * @Date: 2024-08-09 15:40:09
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2024-09-25 16:47:12
 * @Description: 请填写简介
-->
<script setup lang="ts">
import { ref, reactive, unref, toRefs, toRef, toValue, toRaw, watch, watchEffect, defineModel } from 'vue'

const props = defineProps<{ msg: string }>()
console.log('props----', props)
let count = ref(0)
let toValueData = unref(count)
console.log('toValueData----', toValueData)
const objData = reactive({
  name: 'linhao',
  age: 18,
})
objData.name = '小红'
console.log('objData----', objData.name)
const toRawData = toRaw(objData)
console.log('toRawData----', toRawData.name)
let torefData = toRefs(objData)
let torefData2 = toRef(objData, 'age')
torefData2.value++
objData.name = '234'
console.log('torefs----', torefData)
console.log('torefData2----', torefData2)
const dom1 = ref(null)
watch(dom1, (newVal) => {
  console.log('watch------dom1', newVal)
},{flush: 'post'})
// console.log('dom1----', dom1.value)
watchEffect(() => {
  console.log('watchEffect', count.value)
})
let [dataValue, modelModifiers] = defineModel('countData', {
  type: String,
  default: '',
  required: true,
})
const emit = defineEmits(['changeChildNum'])
const changeData = () => {
  count.value++
  dataValue.value = '我是一个大笨蛋'
  torefData2.value++
  emit('changeChildNum', count.value)
}
console.log('dataValue----', dataValue)
console.log('modelModifiers----', modelModifiers)
</script>

<template>
  <slot name="header" :torefData2="torefData2"></slot>
  <h1>{{ msg }}</h1>

  <div class="card" ref="dom1">
    <button type="button" @click="changeData">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>
  <slot></slot>
  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Learn more about IDE Support for Vue in the
    <a
      href="https://vuejs.org/guide/scaling-up/tooling.html#ide-support"
      target="_blank"
      >Vue Docs Scaling up Guide</a
    >.
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
  <slot name="footer"></slot>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
