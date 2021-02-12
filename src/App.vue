<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Header />
    <div class="content">
      <AddTodo v-on:add-todo="addTodo" />
      <Todos
        v-bind:todos="todos"
        v-on:del-todo="deleteTodo"
        v-on:edit-todo="handleEdit"
      />
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Todos from "./components/Todos.vue";
import AddTodo from "./components/AddTodo";
import Header from "./components/Header";
export default {
  name: "App",
  components: {
    Todos,
    AddTodo,
    Header,
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "todo1",
          completed: false,
        },
        {
          id: 2,
          title: "todo2",
          completed: false,
        },
        {
          id: 3,
          title: "todo3",
          completed: false,
        },
        {
          id: 4,
          title: "todo4",
          completed: false,
        },
      ],
    };
  },
  mounted: function () {
    let todos = JSON.parse(localStorage.getItem("todos"));
    if (todos) {
      this.todos = todos;
      console.log(this.todos);
    } else {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id != id);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    addTodo(todo) {
      this.todos = [...this.todos, todo];
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    handleEdit(editedTodo) {
      let index;
      this.todos.map((todo, i) => {
        if (editedTodo.id == todo.id) {
          index = i;
        }
      });

      console.log(index);

      const newTodoes = [...this.todos];
      newTodoes[index] = editedTodo;
      this.todos = newTodoes;
      console.log(this.todos[index]);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style>
#app {
  color: #2c3e50;
  width: 100%;
}
* {
  margin: 0;
}
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 80%;
  margin: 0 auto;
}
</style>
