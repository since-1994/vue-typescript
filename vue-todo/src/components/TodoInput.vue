<template>
  <div>
    <label for="todo-input"></label>
    <input
      id="todo-input"
      type="text"
      :value="value"
      @input="inputHandler"
      @keyup.enter="addTodo"
    />
    <button @click="addTodo">추가</button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: ["value"],
  methods: {
    inputHandler(e: InputEvent) {
      const eventTarget = e.target as HTMLInputElement;
      this.$emit("input", eventTarget.value);
    },
    addTodo() {
      this.$emit("add");
    },
  },
});
</script>

<style scoped>
</style>