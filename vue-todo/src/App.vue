<template>
  <div>
    <header>
      <h1>Vue Todo with Typescript</h1>
    </header>
    <main>
      <TodoInput v-model="todoText" @add="addTodo"></TodoInput>
      <div>
        <ul>
          <TodoListItem></TodoListItem>
        </ul>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoInput from "./components/TodoInput.vue";
import TodoListItem from "./components/TodoListItem.vue";

export default Vue.extend({
  components: { TodoInput, TodoListItem },
  data() {
    return {
      todoText: "",
    };
  },
  methods: {
    addTodo() {
      const value = this.todoText;
      localStorage.setItem(value, value);
      this.clearInput();
    },
    clearInput() {
      this.todoText = "";
    },
  },
});
</script>

<style scoped>
</style>