<template>
  <div class="home">
    <h1>Vue 3 Todo List</h1>
    <form @submit.prevent="addTodo">
      <label> New todo </label>
      <input name="newTodo" v-model="newTodo" />
      <button>submit</button>
    </form>
    <button @click="deleteTodo">reset</button>
    <ul>
      <li
        v-for="(todo, index) in todoList"
        :key="todo.id"
        :class="{ toggleTodo: todo.done }"
      >
        {{ todo.content }}
        <button @click="toggleTodo(todo)" class="todo">
          x
        </button>
        <button @click="removeTodo(index)">remove todo</button>
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");
    const todoList = ref([]);
    function addTodo() {
      todoList.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }
    function toggleTodo(todo) {
      todo.done = !todo.done;
    }
    function deleteTodo() {
      todoList.value.length = 0;
    }
    // ES6 arrow function
    const removeTodo = (index) => {
      todoList.value.splice(index);
    };
    return {
      newTodo,
      todoList,
      addTodo,
      toggleTodo,
      deleteTodo,
      removeTodo,
    };
  },
};
</script>

<style scoped>
.todo {
  cursor: pointer;
}
.toggleTodo {
  text-decoration: line-through;
  color: red;
}
</style>
