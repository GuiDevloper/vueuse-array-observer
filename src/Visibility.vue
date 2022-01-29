<script setup>
import { toRefs } from 'vue'

const props = defineProps({
  isVisible: Array,
  list: Array
})

const { isVisible, list } = toRefs(props)
</script>

<template>
  <div class="visibility">
    <div v-for="(item, i) in list">
      {{ `${isVisible[i] ? 'Visible' : 'invisible'}: ${item}` }}
    </div>
  </div>
</template>

<style scoped>
.visibility {
  position: fixed;
}
</style>