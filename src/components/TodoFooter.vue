<template lang="pug">
footer.footer
  span.todo-count 剩余
    strong {{ count }}
  ul.filters(@click="emits('changeType', isSel)")
    li
      a(:class="{ selected: isSel === 'all' }" @click="isSel = 'all'" href="javascript:;") 全部
    li
      a(:class="{ selected: isSel === 'no' }" @click="isSel = 'no'" href="javascript:;") 未完成
    li
      a(:class="{ selected: isSel === 'yes' }" @click="isSel = 'yes'" href="javascript:;") 已完成
  button.clear-completed(@click="emits('clear')") 清除已完成
</template>

<script setup>
import { ref, computed } from 'vue'
const isSel = ref('all')
const props = defineProps({ farr: { type: Array, required: true } })
const emits = defineEmits(['changeType', 'clear'])
const count = computed(() => props.farr.length)
</script>
