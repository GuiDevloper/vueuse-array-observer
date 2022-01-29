<script setup>
import { toRefs } from 'vue'

const props = defineProps({
  index: Number
})

const { index } = toRefs(props)
</script>

<template>
  <div class="root">
    <p> Box {{index}}</p>
  </div>
</template>

<style scoped>
.root {
  border: 2px dashed #ccc;
  height: 50px;
  margin: 0 2rem 1rem;
}
</style>