<template>
  <h4>{{ msg }}</h4>

  <p>{{ state1.a }}</p>
  <p>{{ state1.gp.b }}</p>
  <p>{{ state1.gp.f.c }}</p>
  <p>{{ state1.gp.f.s.d }}</p>
  <button @click="change1">reactive change1</button>

  <p>{{ state2.a }}</p>
  <p>{{ state2.gp.b }}</p>
  <p>{{ state2.gp.f.c }}</p>
  <p>{{ state2.gp.f.s.d }}</p>
  <button @click="change2">ref change2</button>

  <p>{{ state3.a }}</p>
  <p>{{ state3.gp.b }}</p>
  <p>{{ state3.gp.f.c }}</p>
  <p>{{ state3.gp.f.s.d }}</p>
  <button @click="change3">shallowReactive change3</button>

  <p>{{ state4.a }}</p>
  <p>{{ state4.gp.b }}</p>
  <p>{{ state4.gp.f.c }}</p>
  <p>{{ state4.gp.f.s.d }}</p>
  <button @click="change4">shallowRef change4</button>

  <p>{{ state5.a }}</p>
  <p>{{ state5.gp.b }}</p>
  <p>{{ state5.gp.f.c }}</p>
  <p>{{ state5.gp.f.s.d }}</p>
  <button @click="change5">triggerRef change5</button>
</template>

<script>
/**
    1.递归监听
        默认情况下，无论是通过ref还是reactive都是递归监听

    2.递归监听存在的问题
        如果数据量比较大，非常消耗性能

    3.非递归监听
        shallowRef / shallowReactive

    4.如何触发非递归监听属性更新界面？
        如果是shallowRef类型数据，可以通过triggerRef来触发

    5.应用场景
        一般情况下，我们使用ref和reactive即可
        只有在需要监听的数据量比较大的时候，我们才使用shallowRef/shallowReactive

    6.shallowRef的本质：
        ref -> reactive
        ref(10) -> reactive({value: 10})
        shallowRef -> shallowReactive
        shallowRef(10) -> shallowReactive({value: 10})
        所以如果是通过shallowRef创建的数据，它监听的是.value的变化
        因为底层本质上value才是第一层
 */
import { reactive, ref, shallowReactive, shallowRef, triggerRef } from 'vue'
export default {
  name: 'Comp6',
  props: ['msg'],
  setup() {
    let state1 = reactive({
      a: 'a',
      gp: {
        b: 'b',
        f: {
          c: 'c',
          s: {
            d: 'd'
          }
        }
      }
    })

    let state2 = ref({
      a: 'a',
      gp: {
        b: 'b',
        f: {
          c: 'c',
          s: {
            d: 'd'
          }
        }
      }
    }) // <=> reactive({value: {....}})

    let state3 = shallowReactive({
      a: 'a',
      gp: {
        b: 'b',
        f: {
          c: 'c',
          s: {
            d: 'd'
          }
        }
      }
    })

    let state4 = shallowRef({
      a: 'a',
      gp: {
        b: 'b',
        f: {
          c: 'c',
          s: {
            d: 'd'
          }
        }
      }
    })

    let state5 = shallowRef({
      a: 'a',
      gp: {
        b: 'b',
        f: {
          c: 'c',
          s: {
            d: 'd'
          }
        }
      }
    })

    // 都是内部做了递归，把每一层都包装成了proxy对象，所以很耗性能
    console.log(state1)
    console.log(state1.gp)
    console.log(state1.gp.f)
    console.log(state1.gp.f.s)

    // shallowReactive
    console.log(state3) // 只有第一层被包装成了proxy
    console.log(state3.gp)
    console.log(state3.gp.f)
    console.log(state3.gp.f.s)

    function change1() {
      state1.a = 1
      state1.gp.b = 2
      state1.gp.f.c = 3
      state1.gp.f.s.d = 4
    }

    function change2() {
      state2.value.a = 1 // ref访问需要加.value
      state2.value.gp.b = 2
      state2.value.gp.f.c = 3
      state2.value.gp.f.s.d = 4
    }

    function change3() {
      //   state3.a = 1
      state3.gp.b = 2
      state3.gp.f.c = 3
      state3.gp.f.s.d = 4
    }

    function change4() {
      // 页面不会发生变化
      //   state4.value.a = 1
      //   state4.value.gp.b = 2
      //   state4.value.gp.f.c = 3
      //   state4.value.gp.f.s.d = 4

      // 页面会发生变化
      state4.value = {
        a: '1',
        gp: {
          b: '2',
          f: {
            c: '3',
            s: {
              d: '4'
            }
          }
        }
      }

      // 注意点：
      // 如果是通过shallowRef创建数据，
      // 那么vue监听的是.value的变化，并不是第一层的变化
      console.log(state4)
      console.log(state4.value.gp)
      console.log(state4.value.gp.f)
      console.log(state4.value.gp.f.s)
    }

    function change5() {
      state5.value.gp.f.s.d = 4
      // 注意点： vue3只提供了triggerRef的方法，没有提供triggerReactive.
      //        所以如果是reactive类型的数据，那么是无法主动触发界面更新的。
      triggerRef(state5) //
    }
    return {
      state1,
      change1,
      state2,
      change2,
      state3,
      change3,
      state4,
      change4,
      state5,
      change5
    }
  }
}
</script>
