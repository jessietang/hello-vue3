<template>
  <h4>{{ msg }}</h4>
  <p>{{ age }}</p>
  <button @click="myFn">customRef button</button>
</template>

<script>
import { customRef } from 'vue'
// 自定义一个ref
function myRef(value) {
  return customRef((track, trigger) => {
    return {
      get() {
        track() // 告诉vue这个数据是需要追踪变化的
        console.log('get', value)
        return value
      },
      set(newValue) {
        console.log('set', value)
        value = newValue
        trigger() // 告诉vue触发界面更新
      }
    }
  })
}
export default {
  name: 'Comp11',
  props: ['msg'],
  setup() {
    let age = myRef(18)

    const myFn = () => {
      age.value += 1
    }

    return {
      age,
      myFn
    }
  }
}
</script>
