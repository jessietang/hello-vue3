<template>
  <h4>{{ msg }}</h4>
  <p>{{ state }}</p>
  <button @click="myFn">toRefs myFn</button>
</template>

<script>
import { reactive, toRefs } from 'vue'
export default {
  name: 'Comp10',
  props: ['msg'],
  setup() {
    let obj = { name: 'jessie', age: 26 }
    let state = toRefs(obj)

    /**
toRefs：  结论： 如果利用toRefs将某一个对象中的属性变成响应式的数据，
                  我们修改响应式的数据是会影响到原始数据的。
                  但是，如果响应式的数据是通过toRefs创建的，那么修改了数据并不会触发ui界面的更新。！！！
 */
    const myFn = () => {
      state.name.value = 'yy' // 注意，是state.value.myField
      state.age.value = 10 // 注意，是state.value.myField

      console.log(obj)
      console.log(state)
    }

    return {
      state,
      myFn
    }
  }
}
</script>
