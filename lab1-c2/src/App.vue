<script setup>
import Pomodoro from './components/TimerComponentes/Pomodoro.vue'
</script>

<template>
  <div class="container">
    <h1>Pomodoro Day</h1>
    <Pomodoro />
  </div>

  <footer>
      Noé Isaí Hernández Rivas - Eduardo Antonio Fuentes Melara
  </footer>
</template>

<style>
body {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
  background-color: #F8F4EC; /* 60% */
}

.container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;

  /* 🔥 esto lo sube más arriba */
  justify-content: flex-start;
  padding-top: 60px;
}

/* TÍTULO */
h1 {
  color: #43334C;
  margin-bottom: 20px;
}

/* FOOTER */
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  background-color: #43334C; /* 30% */
  color: white;
  text-align: center;
  padding: 12px;
  font-size: 14px;
}
</style>