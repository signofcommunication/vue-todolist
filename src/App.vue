<template>
  <div id="app">
    <h1>Todo List</h1>
    <div class="input-container">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        placeholder="Add a new task"
      />
      <button @click="addTodo">Add</button>
    </div>

    <ul v-if="todos.length === 0">
      <li>No tasks added yet.</li>
    </ul>
    <ul>
      <li v-for="(todo, index) in todos" :key="index" class="todo-item">
        <span
          :class="{ completed: todo.completed }"
          @click="toggleComplete(index)"
        >
          {{ todo.text }}
        </span>
        <button @click="removeTodo(index)" class="delete-btn">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: []
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({
          text: this.newTodo,
          completed: false
        });
        this.newTodo = '';
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    toggleComplete(index) {
      this.todos[index].completed = !this.todos[index].completed;
    }
  }
};
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: #f0f4f8;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

#app {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
}

h1 {
  text-align: center;
  color: #333;
}

.input-container {
  display: flex;
  gap: 10px;
}

input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 16px;
}

button {
  background-color: #5cb85c;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #4cae4c;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

li {
  color: black
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin-bottom: 10px;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 4px;
  transition: background-color 0.3s;
  color: black;
}

.todo-item:hover {
  background-color: #f1f1f1;
}

.completed {
  text-decoration: line-through;
  color: #888;
}

.delete-btn {
  background-color: #d9534f;
  border: none;
  color: white;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
}

.delete-btn:hover {
  background-color: #c9302c;
}
</style>
