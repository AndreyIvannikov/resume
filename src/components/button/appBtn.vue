<template>
  <button
    :class="['btn', typeBtn ]"
    :disabled="isLengthText"
    @click="$emit('action')"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
    emits:['action'],
  props: {
    text: String,
    typeBtn: String,
    isLengthText:Boolean
  }
};
</script>

<style lang="scss" scoped>
</style>