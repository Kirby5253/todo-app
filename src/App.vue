<template>
  <div>
    <h1>Kirby's Todo App</h1>
    <md-field>
      <md-input
        class="todo-input"
        v-model="currentTodo"
        @keydown.enter="addTodo()"
        placeholder="Add an item to the todo list"
      ></md-input>
    </md-field>

    <div class="todos">
      <md-card
        class="card"
        v-for="todo in todos"
        :key="todo.id"
        md-with-hover
        :class="{complete: todo.completed}"
      >
        <div class="todo-content">
          <input class="complete-checkbox" type="checkbox" @click="completeTodoItem(todo)" />
          <span @dblclick="editTodoItem(todo)">
            <p>{{todo.label}}</p>
            <input
              class="edit-box"
              :class="{editing: todo.edit}"
              v-model="editTodo"
              @keydown.enter="editCompleted(todo)"
            />
          </span>
          <button
            class="edit-button"
            :class="{editing: todo.edit}"
            @click="editCompleted(todo)"
          >Cancel</button>
          <button class="delete-button" @click="removeTodo(todo)">
            <md-icon>delete</md-icon>
          </button>
        </div>
      </md-card>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
      editTodo: ""
    };
  },
  methods: {
    addTodo() {
      if (this.currentTodo.length > 0) {
        this.todos.push({
          id: this.todos.length,
          label: this.currentTodo,
          completed: false,
          edit: false
        });
        this.currentTodo = "";
      }
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodoItem(todo) {
      var index = this.todos.indexOf(todo);
      this.todos[index].edit = true;
      console.log(todo);
    },
    editCompleted(todo) {
      var index = this.todos.indexOf(todo);
      if (this.editTodo.length > 0) {
        this.todos[index].label = this.editTodo;
        this.editTodo = "";
      }
      this.todos[index].edit = false;
    },
    completeTodoItem(todo) {
      var index = this.todos.indexOf(todo);
      if (!this.todos[index].completed) {
        this.todos[index].completed = true;
      } else {
        this.todos[index].completed = false;
      }
      console.log(todo);
    }
  }
};
</script>

<style>
html {
  display: flex;
  justify-content: center;
}
body {
  color: white;
  width: 80%;
  font-size: 24px;
}
p {
  margin: 0;
  margin-right: 40px;
}
.todo-content {
  display: flex;
  align-items: center;
  font-size: 18px;
}
.card {
  padding: 20px;
  margin-bottom: 5px;
}
.complete-checkbox {
  margin-right: 20px;
}
.delete-button {
  position: absolute;
  right: 20px;
  background-color: #424242;
  border: none;
  color: white;
}
.delete-button:hover {
  border-radius: 5px;
  background-color: #636363;
  cursor: pointer;
  color: white;
}
.todo-input {
  margin-top: 20px;
}
.edit-box {
  display: none;
  position: absolute;
  left: 58px;
  width: 400px;
}
.edit-button {
  display: none;
  position: absolute;
  right: 75px;
  margin-right: 20px;
}
.editing {
  display: inline;
}
.complete {
  opacity: 40%;
  text-decoration: line-through;
}
</style>
