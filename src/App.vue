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
        <div>
          <input class="complete-checkbox" type="checkbox" @click="completeTodoItem(todo)" />
          <span @dblclick="editTodoItem(todo)">
            {{todo.label}}
            <input class="edit-box" />
          </span>
          <button class="delete-button" @click="removeTodo(todo)">Delete</button>
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
      currentTodo: ""
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
      this.editTodoItem = index;
      this.todos[index].edit = true;
      console.log(todo);
    },
    editCompleted(todo) {
      var index = this.todos.indexOf(todo);
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
.card {
  padding: 20px;
}
.complete-checkbox {
  margin-right: 20px;
}
.delete-button {
  position: absolute;
  right: 20px;
}
.todo-input {
  margin-top: 20px;
}
.edit-box {
  display: none;
}
.editing {
  display: inline;
}
.complete {
  opacity: 40%;
  text-decoration: line-through;
}
</style>
