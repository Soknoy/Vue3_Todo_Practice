<template>
  <div class="about">
    <h1>Todo list with Reactive</h1>
    <form>
      <label>new todo</label>
      <input name="newTodo" v-model="todo" />
      <button class="todo" @click.prevent="addTodo">Submit</button>
    </form>
    <button @click="resetTodo" class="todo">Reset</button>
    <button @click="markAllTodo">all done</button>
    <ul>
      <li
        v-for="(todo, index) in todoList"
        :key="todo.id"
        :class="{ toggleTodo: todo.done }"
      >
        {{ todo.content }}
        <button @click="deleteTodo(index)">remove</button>
        <button @click="toggleDone(todo)">done</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { reactive, toRefs } from "vue";

export default {
  setup() {
    const data = reactive({
      todo: "",
      todoList: [],
    });
    const addTodo = () => {
      data.todoList.push({
        id: Date.now(),
        content: data.todo,
        done: false,
      });
      data.todo = "";
    };
    const resetTodo = () => {
      data.todoList.length = 0;
    };
    const deleteTodo = (index) => {
      data.todoList.splice(index, 1);
    };
    const toggleDone = (todo) => {
      todo.done = !todo.done;
    };
    const markAllTodo = () => {
      data.todoList.forEach((todo) => {
        todo.done = true;
      });
    };

    return {
      ...toRefs(data),
      addTodo,
      resetTodo,
      deleteTodo,
      toggleDone,
      markAllTodo,
    };
  },
};
</script>
<style scoped>
.toggleTodo {
  text-decoration: line-through;
  color: red;
}
.todo {
  cursor: pointer;
}
</style>
