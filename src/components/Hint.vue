<template>
  <div class="hint box is-large">
      <!-- <span class="icon">❓</span> -->
      {{hint}}
  </div>
</template>

<script>
export default {
    props: {
        hint: {
            type: String,
            required: true
        }
    }
}
</script>

<style>
.hint.box {
    background-color: #000;
    color: white;
}
</style>