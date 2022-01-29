<script setup>
import Comp from './Comp.vue'
import Visibility from './Visibility.vue'

import { ref, reactive, onBeforeUpdate, watchEffect } from 'vue'
import { useIntersectionObserver } from '@vueuse/core'

const isVisible = ref([])
const list = reactive([1])
const itemRefs = ref([])

onBeforeUpdate(() => {
  itemRefs.value = []
})

watchEffect(() => {
  list.forEach((_el, i) => {
    useIntersectionObserver(
      itemRefs.value[i],
      ([{ isIntersecting }]) => {
        isVisible.value[i] = isIntersecting
      }
    )
  })
}, { flush: 'post' })

const setItemRef = el => {
  if (el) {
    itemRefs.value.push(el)
  }
}
const addToList = () => {
  const lastItem = list[list.length - 1]
  list.push(lastItem + 1)
}
</script>

<template>
  <div class="root">
    <Visibility :isVisible="isVisible" :list="list" />
    <div class="btns">
      <button @click="addToList">Add</button>
      <button @click="list.pop()">Remove</button>
    </div>
    <Comp
      v-for="item in list"
      :ref="setItemRef"
      :index="item"
    />
  </div>
</template>

<style scoped>
.btns {
  margin-bottom: 50px;
}
</style>