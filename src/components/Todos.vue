<template>
  <div class="todos">
    <div class="wrap">
      <div v-bind:key="todo.id" v-for="todo in todos">
        <Todo
          v-bind:todo="todo"
          v-on:del-todo="$emit('del-todo', todo.id)"
          v-on:edit-todo="handleEdit"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";
export default {
  name: "Todos",
  components: {
    Todo,
  },
  props: ["todos"],
  methods: {
    handleEdit(editedTodo) {
      this.$emit("edit-todo", editedTodo);
    },
  },
};
</script>

<style scoped>
.todos {
  /* display: flex;
        align-items: center;
        justify-content: center; */
  width: 100%;
}

h1 {
  font-size: 40px;
}
ul {
  padding: 0;
}
</style>
