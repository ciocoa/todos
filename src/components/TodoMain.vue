<template lang="pug">
ul.todo-list
  li(:class="{ completed: obj.isDone }" v-for="obj in arr" :key="obj.id")
    .view
      input.toggle(type="checkbox" v-model="obj.isDone")
      label {{ obj.name }}
      button.destroy(@click="emits('del', obj.id)")
</template>

<script setup>
defineProps({ arr: { type: Array, required: true } })
const emits = defineEmits(['del'])
</script>
