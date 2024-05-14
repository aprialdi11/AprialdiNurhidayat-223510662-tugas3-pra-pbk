<script setup>
import { ref } from 'vue';

const todos = ref([
  { id: 1, text: 'Example Todo 1', completed: false },
  { id: 2, text: 'Example Todo 2', completed: true },
]);

let newTodo = ref('');

function addTodo() {
  if (newTodo.value.trim() !== '') {
    todos.value.push({ id: todos.value.length + 1, text: newTodo.value, completed: false });
    newTodo.value = '';
  }
}

function deleteTodo(id) {
  todos.value = todos.value.filter(todo => todo.id !== id);
}

function toggleTodoStatus(id) {
  todos.value = todos.value.map(todo => {
    if (todo.id === id) {
      todo.completed = !todo.completed;
    }
    return todo;
  });
}
</script>

<template>
  <div class="todo-container">
    <h2>Todo List</h2>

    <!-- Input for Adding New Todo -->
    <div class="input-container">
      <input type="text" v-model="newTodo" placeholder="Enter your todo..." />
      <button @click="addTodo">Add Todo</button>
    </div>

    <!-- List of Todos -->
    <ul>
      <li v-for="todo in todos" :key="todo.id" class="todo-item">
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <div>
          <button @click="toggleTodoStatus(todo.id)">
            {{ todo.completed ? 'Mark Incomplete' : 'Mark Complete' }}
          </button>
          <button @click="deleteTodo(todo.id)">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
/* Container Styles */
.todo-container {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 8px;
  background-color: #81e2a6;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

/* Input Styles */
.input-container {
  display: flex;
  margin-bottom: 20px;
}

input[type="text"] {
  flex: 1;
  padding: 10px;
  border: 1px solid #ced4da;
  border-radius: 4px 0 0 4px;
}

button {
  padding: 10px 20px;
  background-color: #28a745;
  color: #fff;
  border: none;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #218838;
}

/* Todo List Styles */
ul {
  list-style-type: none;
  padding: 0;
}

.todo-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #ddd;
  padding-bottom: 8px;
}

.completed {
  text-decoration: line-through;
}
</style>
