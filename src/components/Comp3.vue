<template>
  <h4>{{ msg }}</h4>
  <p>{{ arr }}</p>
  <p>modelName: {{ modelName }}</p>
  <button @click="updateModelName">updateModelName</button>
  <input type="text" v-model="newStu.id" />
  <input type="text" v-model="newStu.name" />
  <input type="text" v-model="newStu.age" />
  <button @click="addStu">addStu</button>
  <p
    v-for="(stu, index) in state1.stus"
    :key="stu.id"
    @click="removeStu(index)"
  >
    {{ stu.id }}-{{ stu.name }}-{{ stu.age }}
  </p>
</template>
<script>
import { reactive, ref } from 'vue'
export default {
  name: 'Comp3',
  props: ['msg'],
  /**
   * 1.什么是reactive？
   * - reactive是vue3中提供的实现响应式数据的方法
   * - 在vue2中响应式数据是通过defineProperty来实现的，
   *   而在vue3中响应式数据是通过ES6的Proxy来实现的
   *
   * 2.reactive注意点：
   * - reactive参数必须是对象（json/arr）
   * - 如果给reactive传递了其他对象
   *    + 默认情况下修改对象，界面不会自动更新
   *    + 如果想更新，可以通过重新赋值的方式来实现
   */
  setup() {
    const arr = reactive([1, 2, 3])
    console.log('arr', arr)

    let { modelName, updateModelName } = useUpdateModelName()
    let { state1, removeStu } = useRemoveStu()
    let { newStu, addStu } = useAddStudent(state1)

    return {
      arr,
      state1,
      newStu,
      addStu,
      removeStu,
      modelName,
      updateModelName
    }
  }
}

function useUpdateModelName() {
  const modelName = ref('123')

  function updateModelName() {
    modelName.value = modelName.value + 'hhh' // !!!
  }
  return { modelName, updateModelName }
}

function useAddStudent(state1) {
  const newStu = reactive({
    id: '',
    name: '',
    age: ''
  })

  function addStu(e) {
    e.preventDefault()
    const stu = Object.assign({}, newStu)
    state1.stus.push(stu)
    newStu.id = ''
    newStu.name = ''
    newStu.age = ''
  }

  return { newStu, addStu }
}

function useRemoveStu() {
  const state1 = reactive({
    stus: [
      {
        id: 0,
        name: 'zs',
        age: 13
      }
    ]
  })
  function removeStu(index) {
    console.log('remove', index)
    state1.stus = state1.stus.filter((_, i) => i !== index)
  }

  return {
    state1,
    removeStu
  }
}
</script>
