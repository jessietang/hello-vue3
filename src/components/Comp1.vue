<template>
  <h4>{{ msg }}</h4>
  <button @click="count++">count is: {{ count }}</button>
  <p>{{ info.name }}</p>
  <p>{{ x }}, {{ y }}</p>
</template>

<script>
function useMousePosition() {
  const pos = reactive({
    x: 0,
    y: 0
  })

  const updatePos = (e) => {
    pos.x = e.pageX
    pos.y = e.pageY
    console.log('pos', pos)
  }

  onMounted(() => {
    document.addEventListener('mousemove', updatePos)
  })

  onUnmounted(() => {
    document.removeEventListener('mousemove', updatePos)
  })

  // return pos
  return toRefs(pos) // toRefs API 用来提供解决此约束的办法——它将响应式对象的每个 property 都转成了相应的 ref
}

import { reactive, computed, ref, onMounted, onUnmounted, toRefs } from 'vue'
export default {
  props: ['msg'],
  name: 'Comp1',
  data() {
    return {
      m1: 'mmmmm11111'
    }
  },
  setup() {
    const count = ref(10)
    const info = reactive({
      name: 'zs',
      age: 26,
      sex: 'female',
      time: null
    })
    console.log('count', count.value)
    console.log('info-name', info.name)

    // 只使用 reactive 的问题是，使用组合函数时必须始终保持对这个所返回对象的引用以保持响应性。这个对象不能被解构或展开
    // 这里会丢失响应性!
    // const { x, y } = useMousePosition()
    // return {
    //   x,
    //   y,
    // }

    // 这里会丢失响应性!
    // return {
    //   ...useMousePosition(),
    // }

    // toRefs API 用来提供解决此约束的办法——它将响应式对象的每个 property 都转成了相应的 ref
    const { x, y } = useMousePosition()

    return {
      count,
      info,
      // pos: useMousePosition()
      x,
      y
    }
  }
}
</script>
