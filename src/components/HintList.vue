<template>
  <div class="hint-list">
      <hint v-for="(hint, index) in hints" :hint="hint" :key="index"></hint>
  </div>
</template>

<script>
import hint from './Hint.vue'
export default {
    components: {
        hint
    },
    props: {
        hints: {
            type: Array,
            required: true
        }
    }
}
</script>

<style>
.hint-list {
    background-color: #000
}
</style>
