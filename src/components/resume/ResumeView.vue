<template>
  <div class="card card-w70">
    <component
      v-for="(key, idx) in elements"
      :key="idx"
      :is="key.type + '-' + 'resume'"
      :value="key.value"
    >
    </component>
    <h3 v-if="elements.length === 0">
      Добавьте первый блок, чтобы увидеть результат
    </h3>
  </div>
</template>

<script>
import TextResume from "./text/TextResume";
import SubtitleResume from "./subtitle/SubtitleResume";
import TitleResume from "./name/TitleResume.vue";
import AvatarResume from "./avatar/AvatarResume";
export default {
  components: {
    TextResume,
    SubtitleResume,
    TitleResume,
    AvatarResume,
  },
  props:{
      elements:Array
  },
};
</script>

<style lang="scss" scoped>
</style>