<template>
  <div class="app-container">
    <h1>🎬 Gestionnaire de Films</h1>

    <p :class="{ active: count > 5 }">Compteur : {{ count }}</p>

    <div class="buttons">
      <button @click="increment">➕</button>
      <button @click="decrement">➖</button>
      <button @click="sortMovies">🔀 Trier</button>
    </div>

    <form @submit.prevent="addMovie" class="movie-form">
      <input
        type="text"
        placeholder="Ajouter un film..."
        v-model="movieName"
      />
      <button type="submit">Ajouter</button>
    </form>

    <div class="message" :class="{ positive: count >= 5, negative: count < 5 }">
      {{ count >= 5
        ? '👏 Bravo ! Vous avez cliqué plus que 5 fois !'
        : '💡 Vous avez cliqué moins de 5 fois.' }}
    </div>

    <ul class="movie-list">
      <li v-for="movie in movies" :key="movie">
        <span>{{ movie }}</span>
        <button class="delete-btn" @click="deleteMovie(movie)">🗑️</button>
      </li>
    </ul>
  </div>
  <div class="highlight-box">
  <h2>🎬 Acteur de la semaine</h2>
  <ul>
    <li><strong>Nom :</strong> {{ person.lastName }}</li>
    <li><strong>Âge :</strong> {{ person.age }}</li>
  </ul>
  <button @click.prevent="randomAge" class="highlight-button">Changer l'âge</button>
</div>



</template>

<script setup>
import { ref } from 'vue'

const count = ref(0)
const increment = () => count.value++
const decrement = () => count.value--

const movies = ref(['TITANIC', 'MATRIX', 'GRAGE'])

const movieName = ref('')

const sortMovies = () => {
  movies.value.sort((a, b) => a.localeCompare(b))
}

const addMovie = () => {
  if (movieName.value.trim()) {
    movies.value.push(movieName.value.trim())
    movieName.value = ''
    sortMovies()
  }
}

const deleteMovie = (movie) => {
  movies.value = movies.value.filter((m) => m !== movie)
}

const person = ref({
  firstName : 'John',
  lastName: 'Doe',
  age: 10
})

const randomAge = () => {
  person.value.age = Math.round(Math.random() * 100)
}
</script>

<style scoped>
.app-container {
  max-width: 600px;
  margin: 40px auto;
  padding: 24px;
  background: #f9f9f9;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  font-family: "Segoe UI", sans-serif;
  color: #333;
}

h1 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 24px;
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 20px;
}

button {
  background-color: #3498db;
  border: none;
  color: white;
  padding: 10px 16px;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s;
}

button:hover {
  background-color: #2980b9;
}

button.delete-btn {
  background-color: #e74c3c;
  padding: 6px 10px;
}

button.delete-btn:hover {
  background-color: #c0392b;
}

.movie-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.movie-form input {
  flex: 1;
  padding: 8px 12px;
  border: 1px solid #ccc;
  border-radius: 6px;
}

.movie-list {
  list-style: none;
  padding: 0;
}

.movie-list li {
  background: #fff;
  margin-bottom: 10px;
  padding: 10px 14px;
  border-radius: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.08);
}

.active {
  color: green;
  font-weight: bold;
}

.message {
  text-align: center;
  margin-bottom: 20px;
  font-weight: bold;
}

.message.positive {
  color: green;
}

.message.negative {
  color: #e67e22;
}


.highlight-box {
  background-color: #fffbe6;
  border: 1px solid #f1c40f;
  padding: 20px;
  margin: 40px auto 0;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(241, 196, 15, 0.2);
  max-width: 600px;
  text-align: left;
}

.highlight-box h2 {
  margin-top: 0;
  color: #d4ac0d;
  text-align: center;
}

.highlight-box ul {
  list-style: none;
  padding: 0;
  margin: 10px 0 20px 0;
}

.highlight-box li {
  margin-bottom: 8px;
  font-size: 16px;
}

.highlight-box li strong {
  color: #333;
}

.highlight-button {
  background-color: #f39c12;
  color: white;
  padding: 10px 16px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  display: block;
  margin: 0 auto;
  transition: background-color 0.2s;
}

.highlight-button:hover {
  background-color: #e67e22;
}

</style>
