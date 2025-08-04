<template>
  <main class="container">
    <article class="todo-app">
      <header>
        <h1>📝 Ma To-Do List</h1>
        <p class="description">Gérez vos tâches avec élégance et simplicité.</p>
      </header>

      <form @submit.prevent="addTodo" class="todo-form">
        <input
          type="text"
          placeholder="Ajouter une tâche..."
          v-model="todoName"
        />
        <button :disabled="todoName.length === 0" type="submit">Ajouter</button>
      </form>

      <label class="checkbox-line">
        <input type="checkbox" v-model="hideCompleted" />
        Masquer les tâches complétées
      </label>

      <section v-if="todos.length === 0" class="empty">
        🎉 Vous n'avez aucune tâche en attente !
      </section>

      <ul v-else class="todo-list">
        <li
          v-for="todo in sortTodos()"
          :key="todo.date"
          :class="{ completed: todo.completed }"
        >
          <label class="todo-item">
            <input type="checkbox" v-model="todo.completed" />
            <span>{{ todo.title }}</span>
          </label>
        </li>
      </ul>
    </article>
  </main>
</template>

<script setup>
import { ref } from 'vue'

const todoName = ref('')
const hideCompleted = ref(false)

const todos = ref([
  { title: 'Faire les courses', completed: true, date: 1 },
  { title: 'Apprendre Vue 3', completed: false, date: 2 },
  { title: 'Boire un café ☕', completed: false, date: 3 }
])

const addTodo = () => {
  if (todoName.value.trim()) {
    todos.value.push({
      title: todoName.value.trim(),
      completed: false,
      date: Date.now()
    })
    todoName.value = ''
  }
}

const sortTodos = () => {
  const sorted = todos.value.toSorted((a, b) => a.completed - b.completed)
  return hideCompleted.value ? sorted.filter(t => !t.completed) : sorted
}
</script>

<style scoped>
.todo-app {
  max-width: 600px;
  margin: 3rem auto;
  padding: 2rem;
  border-radius: 1rem;
  background: var(--pico-background-color);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
}

header {
  text-align: center;
  margin-bottom: 2rem;
}

.description {
  color: #888;
  font-size: 0.95rem;
}

.todo-form {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.todo-form input {
  flex: 1;
}

.checkbox-line {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
  font-size: 0.9rem;
  color: #555;
}

.todo-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1rem;
  border-radius: 0.75rem;
  background: var(--pico-muted-color);
  margin-bottom: 0.75rem;
  transition: all 0.3s ease;
}

.todo-item:hover {
  background: var(--pico-muted-border-color);
}

.completed span {
  text-decoration: line-through;
  opacity: 0.5;
}

.empty {
  text-align: center;
  padding: 2rem 0;
  font-style: italic;
  color: #777;
  background: var(--pico-muted-color);
  border-radius: 0.75rem;
}
</style>
