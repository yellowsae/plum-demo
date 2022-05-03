<template>
  <input type="text" v-model="todoMsg">
  <button @click="add">添加</button>
  <button @click="clearHasDone">清理</button>
  <div v-if="lists.length">
    <div v-for="(item, index) in lists" :key="item.msg">
      <input type="checkbox" v-model="item.done" />
      <span :class="{ done: item.done }">{{ item.msg }}</span>
      <span @click="deleteItem(index)">❌</span>
    </div>
    <div>
      <span>全选</span>
      <input type="checkbox" v-model="isAllDone">
      <span> {{ isDone }} /{{ lists.length }}</span>
    </div>
  </div>
  <div v-else>
    <span>暂无数据</span>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from "vue"

interface TodoItem {
  msg: string
  done: boolean
}


const todoMsg = ref('')

const lists = ref<TodoItem[]>([
  {
    msg: '事件1',
    done: false
  }, {
    msg: '事件2',
    done: true
  }, {
    msg: '事件3',
    done: false
  }
])


const isDone = computed(() => lists.value.filter(item => item.done).length)


const isAllDone = computed<boolean>({
  get() {
    return isDone.value === lists.value.length
  },
  set(value) {
    lists.value.forEach(item => item.done = value)
  }
})

const add = () => {
  if(todoMsg.value) {
    lists.value.push({
      msg: todoMsg.value,
      done: false
    })
  }
  todoMsg.value = ''
}

const clearHasDone = () => {
  lists.value = lists.value.filter(item => !item.done)
}

const deleteItem = (index: number) => {
  lists.value.splice(index, 1)
}
</script>

<style scoped>
.done {
  text-decoration: line-through;
  color: gray
}
</style>
