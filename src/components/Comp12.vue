<template>
  <h4>{{ msg }}</h4>
  <ul>
    <li v-for="d in state" :key="d.id">{{ d.name }}</li>
  </ul>
</template>

<script>
import { customRef, ref } from 'vue'
// 自定义一个ref
function myRef(value) {
  return customRef((track, trigger) => {
    fetch(value)
      .then((res) => {
        return res.json()
      })
      .then((data) => {
        console.log('data', data)
        value = data
        trigger() //  告诉vue触发界面更新
      })
      .catch((e) => {
        console.log(e)
      })
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
  name: 'Comp12',
  props: ['msg'],
  setup() {
    let state = myRef('../../public/data.json')

    // fetch('../../public/data.json')
    //   .then((res) => {
    //     return res.json()
    //   })
    //   .then((data) => {
    //     console.log('data', data)
    //     state.value = data
    //   })
    //   .catch((e) => {
    //     console.log(e)
    //   })

    return {
      state
    }
  }
}
</script>
