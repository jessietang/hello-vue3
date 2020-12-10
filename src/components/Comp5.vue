<template>
  <h4>{{ msg }}</h4>
  <p>{{ age }}</p>
  <button @click="myFn">myFn</button>
</template>
<script>
/**
 * 1.ref和reactive的区别：
 *  如果在template里面使用的是ref类型的数据，那么vue会自动帮我们添加.value
 *  如果再template里面使用的是reactive类型的数据，那么vue不会自动帮我们添加.value
 *
 * 2.vue是如何决定是否需要添加.value的？
 *  vue在解析数据之前，会自动判断这个数据是否是ref类型的，
 *  如果是，则自动添加.value, 如果不是就不添加.value
 *
 * 3.vue是如何判断当前的数据是否是ref类型的呢？
 *  通过当前数据的__v_ref来判断的
 *  如果有这个私有的属性，并且取值为true，那么就代表是一个ref类型的数据
 *
 * 4.我们怎么去判断当前数据是ref类型还是reactive类型呢?
 *  vue给我们提供了isRef和isReactive两个方法
 */
import { ref, reactive, isRef, isReactive } from 'vue'
export default {
  name: 'Comp5',
  props: ['msg'],
  setup() {
    let age = ref(100)

    console.log(age) // {...,__v_isRef: true}

    console.log(isRef(age))
    console.log(isReactive(age))

    let age2 = reactive({
      value: 110
    })

    console.log(isRef(age2))
    console.log(isReactive(age2))

    // let age = reactive({
    //   value: 100
    // }) // template里面如果还是<p>{{ age }}</p>，显示的就是： { "value": 100 }

    function myFn() {
      age.value = 101
    }

    return {
      age,
      myFn
    }
  }
}
</script>
