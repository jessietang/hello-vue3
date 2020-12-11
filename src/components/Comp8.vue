<template>
  <h4>{{ msg }}</h4>
  <p>{{ state }}</p>
  <button @click="myFn">myFn markRaw</button>
</template>

<script>
import { reactive, markRaw } from 'vue'
export default {
  name: 'Comp8',
  props: ['msg'],
  setup() {
    let obj = { name: 'jessietang', age: 26 }
    obj = markRaw(obj) // markRow是数据永远不被追踪
    let state = reactive(obj)

    function myFn() {
      state.name = 'zs'
    }
    return {
      state,
      myFn
    }
  }
}
</script>
