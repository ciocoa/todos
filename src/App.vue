<template lang="pug">
section.todoapp
  TodoHeader(:arr="list" @create="createFn")
  TodoMain(:arr="showArr" @del="deleteFn")
  TodoFooter(:farr="showArr" @changeType="typeFn" @clear="clearFn")
</template>

<script setup>
import './assets/base.css'
import './assets/index.css'
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
import { ref, computed, watch } from 'vue'
const list = ref(JSON.parse(localStorage.getItem('todolist')) || [])
const getSel = ref('all')
const createFn = task =>
  list.value.push({
    id: list.value.length === 0 ? 100 : list.value[list.value.length - 1].id + 1,
    name: task,
    isDone: false
  })
const deleteFn = id =>
  list.value.splice(
    list.value.findIndex(obj => obj.id === id),
    1
  )
const typeFn = str => (getSel.value = str)
const clearFn = () => (list.value = list.value.filter(obj => obj.isDone === false))
const showArr = computed(() => {
  if (getSel.value === 'yes') return list.value.filter(obj => obj.isDone === true)
  else if (getSel.value === 'no') return list.value.filter(obj => obj.isDone === false)
  else return list.value
})
watch([list, list.value], () => localStorage.setItem('todolist', JSON.stringify(list.value)))
</script>
