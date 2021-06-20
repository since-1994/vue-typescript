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

const STORAGE_KEY = "todo-vue-key";

const storage = {
  save(todos: any[]) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todos));
  },
  fetch() {
    const todoItems = localStorage.getItem(STORAGE_KEY) || "[]";
    const result = JSON.parse(todoItems);
    return result;
  },
};

export default Vue.extend({
  components: { TodoInput, TodoListItem },
  data() {
    return {
      todoText: "",
      todoItems: [] as any,
    };
  },
  methods: {
    addTodo() {
      const value = this.todoText;
      this.todoItems.push(value);
      storage.save(this.todoItems);
      this.clearInput();
    },
    clearInput() {
      this.todoText = "";
    },
    fetchTodoItems() {
      this.todoItems = storage.fetch();
    },
  },
  created() {
    this.fetchTodoItems();
  },
});
</script>

<style scoped>
</style>