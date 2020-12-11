<template>
  <h4>{{ msg }}</h4>
  <p>{{ state }}</p>
  <button @click="myFn">myFn</button>
</template>

<script>
import { reactive, ref, toRaw } from 'vue'
export default {
  name: 'Comp7',
  props: ['msg'],
  setup() {
    let obj = {
      name: 'jessie',
      age: 26
    }
    /**
    ref/reactive数据类型的特点：
        每次修改都会被追踪，都会更新ui界面，但是这样其实是非常消耗性能的
        所以如果我们有一些操作不需要追踪，不需要更新ui界面，那么这个时候，
        我们就可以通过toRaw方法拿到他的原始数据，对原始数据进行修改
        这样就不会被追踪，这样就不会更新ui界面，这样性能就好了
     */
    let state = reactive(obj)
    let obj2 = toRaw(state)
    console.log('obj ?== obj2 : ', obj === obj2) // true

    function myFn() {
      obj2.name = 'ls'
    }

    // ref本质： reactive
    // ref(obj) -> reactive({value: obj})
    let test = {
      name: 'jessie',
      age: 26
    }
    /**
    注意点：如果想通过toRaw拿到ref类型的原始数据（创建时传入的那个数据）
           那么必须明确的告诉toRaw方法，要获取的是.value的值
           因为经过vue处理之后，.value中保存的才是当初创建时传入的那个原始数据
     */
    let state2 = ref(test)
    let test2 = toRaw(state2)
    console.log('test ?== test2: ', test === test2) // false
    console.log(test)
    console.log(state2)
    console.log(test2)

    return {
      state
    }
  }
}
</script>
