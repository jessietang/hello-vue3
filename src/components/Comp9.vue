<template>
  <h4>{{ msg }}</h4>
  <p>{{ state }}</p>
  <button @click="myFn">ref button</button>

  <p>{{ state2 }}</p>
  <button @click="myFn2">toRef button</button>
</template>

<script>
import { ref, toRef } from 'vue'
/**
ref和toRef区别：
    ref: -> 复制。修改响应式数据不会影响以前的数据
    toRef: -> 引用。修改响应式数据会影响以前的数据
    ref: 数据发生改变，界面就会自动更新
    toRef: 数据发生改变，界面也不会自动更新
 */
export default {
  name: 'Comp9',
  props: ['msg'],
  setup() {
    let obj = { name: 'xiayu', age: 26 }
    let state = ref(obj.name) // ref(xiayu) -> reactive({value: xiayu})

    const myFn = () => {
      /**
            结论： 如果利用ref将某一个对象中的属性变成响应式的数据，
                  我们修改响应式的数据不会影响到原始数据
         */
      state.value = 'zs'
      console.log(obj) // 不变
      console.log(state) // 会改变
    }

    let obj2 = { name: 'xiayu', age: 26 }
    let state2 = toRef(obj2, 'name') // 注意写法
    const myFn2 = () => {
      /**
            结论： 如果利用toRef将某一个对象中的属性变成响应式的数据，
                  我们修改响应式的数据是会影响到原始数据的。
                  但是，如果响应式的数据是通过toRef创建的，那么修改了数据并不会触发ui界面的更新。！！！
         */
      state2.value = 'zs'
      console.log(obj2) // 会变化
      console.log(state2) // 会改变
    }
    return {
      state,
      myFn,
      state2,
      myFn2
    }
  }
}
</script>
