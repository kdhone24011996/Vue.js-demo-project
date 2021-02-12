<template>
  <div
    v-bind:class="{ isCompleted: todo.completed }"
    style="margin-top: 1.5rem"
  >
    <div v-bind:class="{ isEditing: isEditing }">
      <div class="group">
        <div>
          <input
            type="checkbox"
            v-on:change="toggleCompleted"
            v-model="todo.completed"
            :id="id"
            class="my-checkbox"
          />
          <label :for="id">{{ todo.title }}</label>
        </div>
        <div>
          <button @click="edit">EDIT</button>
          <button
            @click="$emit('del-todo', todo.id)"
            style="color: white; background-color: red; opacity: 0.8"
          >
            DELETE
          </button>
        </div>
      </div>
    </div>
    <div v-bind:class="{ isEditing: !isEditing }">
      <input type="text" v-model="title" class="text-input" />
      <button @click="handleSubmit" class="submit-button">submit</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: ["todo"],
  data() {
    return {
      title: this.todo.title,
      id: this.todo.id,
      isEditing: false,
      completed:this.todo.completed
    };
  },
  methods: {
    toggleCompleted() {
      // this.todo.completed = !this.todo.completed;
      console.log(this.todo.completed)
      let todos = JSON.parse(localStorage.getItem("todos"));
      let index;
      todos.map((todo, i) => {
        if (this.todo.id == todo.id) {
          index = i;
        }
      });

      todos[index] = this.todo;
      localStorage.setItem("todos", JSON.stringify(todos));
    },
    edit() {
      console.log(this.title);
      this.isEditing = true;
    },
    handleSubmit() {
      if (!this.title) return;

      const editedTodo = {
        id: this.todo.id,
        title: this.title,
        completed: this.todo.completed,
      };
      this.$emit("edit-todo", editedTodo);
      this.isEditing = false;
    },
  },
};
</script>

<style scoped>
.isCompleted {
  text-decoration: line-through;
}
.isEditing {
  display: none;
  width: 100%;
}

.group {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

label {
  font-size: 2rem;
  margin-left: 0.7rem;
  /* margin-right: 2.5rem; */
}

button {
  padding: 1rem;
  border-radius: 3px;
  background-color: gray;
}
.submit-button {
  padding: 0.7rem 1.5rem;
  background-color: green;
  color: white;
}
.text-input {
  width: 12rem;
  padding: 0.7rem 1rem;
  border-radius: 3px;
  outline-color: #748277;
  margin-right: 2rem;
}

.text-input:focus-within {
  outline-color: #84fa9e;
}

.my-checkbox[type="checkbox"]:before {
  position: relative;
  display: block;
  left: -12px;
  top: -5px;
  width: 26px;
  height: 26px;
  border: 1px solid #ec5426;
  content: "";
  background-color: #f5f5f5;
}

.my-checkbox[type="checkbox"]:checked:after {
  background-color: #ec5426;
  position: relative;
  display: block;
  left: -12px;
  top: -33px;
  width: 26px;
  height: 26px;
  border: 1px solid #ec5426;
  background-image: url("../assets/checked.svg");
  background-repeat: no-repeat;
  background-position: center;
  content: "";
}
</style>
