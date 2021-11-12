<template lang="pug">
header.header
  h1 todos
  input#toggle-all.toggle-all(type="checkbox" v-model="isAll")
  label(for="taggle-all")
  input.new-todo(placeholder="输入任务名称" autofocus @keydown.enter="downFn" v-model="task")
</template>

<script setup>
import { ref, computed } from 'vue'
const props = defineProps({ arr: { type: Array, required: true } })
const emits = defineEmits(['create'])
const task = ref('')
const isAll = computed({
  set: checked => props.arr.forEach(obj => (obj.isDone = checked)),
  get: () => props.arr.length !== 0 && props.arr.every(obj => obj.isDone === true)
})
const downFn = () => {
  if (task.value.trim().length === 0) return alert('not null')
  emits('create', task.value)
  task.value = ''
}
</script>
