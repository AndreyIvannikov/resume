<template>
  <form class="card card-w30" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="select">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model="textField"></textarea>
    </div>
    <button class="btn primary" :disabled="isLengthValue">Добавить</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      select: "title",
      textField: ""
    };
  },
  methods: {
    onSubmit() {
      this.$emit("add-component", {
        value: this.select,
        textField: this.textField
      });
      this.select = "title";
      this.textField = "";
    }
  },
  computed: {
    isLengthValue() {
      return this.textField.length < 3;
    }
  }
};
</script>

<style lang="scss" scoped>
</style>