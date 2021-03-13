<template>
  <h1>Vue 3 ToDo App</h1>
  <form @submit.prevent="addNewTodo">
    <input name="newTodo" v-model="newTodo" />
    <button>Add New ToDo</button>
  </form>
  <h2>model change: {{ newTodo }}</h2>
  <!-- LIST -->
  <button @click="markAllDone()" :disabled="todos.length === 0">
    mark all as done
  </button>
  <ul v-for="(todo, index) in todos" v-bind:key="todo.id" class="todo">
    <li :class="{ done: todo.done }" @click="toggleDone(todo)">
      {{ todo.content }}
      <button @click="removeTodo(index)">remove</button>
    </li>
  </ul>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const todos = ref([]);
    /* const data = reactive({
      newTodo: '',
      todo: []
    }); */
    const newTodo = ref("");
    function addNewTodo() {
      console.log("form submitted");
      console.log(newTodo.value);
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((element) => {
        element.done = true;
      });
    }

    return {
      newTodo,
      addNewTodo,
      todos,
      toggleDone,
      removeTodo,
      markAllDone,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.done {
  text-decoration: line-through;
}
.todo {
  cursor: pointer;
}
</style>
