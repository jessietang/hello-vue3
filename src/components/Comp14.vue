<template>
  <h4>{{ msg }}</h4>
  <p>{{ state }}</p>
  <button @click="myFn">button</button>
</template>
<script>
import { readonly, shallowReadonly, isReadonly } from 'vue'
export default {
  name: 'Comp14',
  props: ['msg'],
  setup() {
    // readonly用于创建一个只读的数据，并且是递归只读
    // let state = readonly({
    //   name: 'jessie',
    //   attr: { age: 26, height: 2.6 }
    // })
    // shallowReadonly: 用于创建一个只读的数据，但是不是递归只读的
    let state = shallowReadonly({
      name: 'jessie',
      attr: { age: 26, height: 2.6 }
    }) // 第一层改不了，第二层可以修改

    // const 和 readonly的区别
    // const: 变量保护，不能给变量重新赋值
    // readonly: 属性保护，不能给属性重新赋值

    // const value = 123
    const value2 = {
      name: 'j',
      age: 1
    }

    const myFn = () => {
      state.name = 'yuyu'
      state.attr.age = 18
      state.attr.height = 1.88

      console.log(state)

      console.log(isReadonly(state))

      //   value = 456 // 报错
      //   console.log(value)

      value2.name = 's'
      value2.age = 2
      console.log(value2) // {name: 's', age: 2}
    }

    return {
      state,
      myFn
    }
  }
}
</script>
