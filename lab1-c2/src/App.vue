<script setup>
import { ref } from 'vue'
import Timer from './components/TimerComponentes/Timer.vue'

// VARIABLES REACTIVAS
const minutos = ref(25)
const error = ref('')
const iniciar = ref(false)
const historial = ref([])

// VALIDACIÓN
function iniciarPomodoro() {
  if (minutos.value <= 0) {
    error.value = 'Debe ser mayor a 0'
    return
  }

  if (minutos.value > 60) {
    error.value = 'Máximo 60 minutos'
    return
  }

  error.value = ''
  iniciar.value = true
}

function guardarHistorial() {
  historial.value.push(`Sesión de ${minutos.value} minutos completada`)
}
</script>

<template>
   <div class="container">
    <h1>Pomodoro</h1>

    <!-- INPUT -->
    <input 
      type="number" 
      v-model="minutos"
    >

    <!-- BOTÓN -->
    <button @click="iniciarPomodoro">
      Iniciar
    </button>

    <!-- ERROR -->
    <p v-if="error" class="error">{{ error }}</p>

    <!-- TIMER -->
    <Timer 
      v-if="iniciar"
      :minutos="minutos"
      @finalizado="guardarHistorial"
    />
  </div>

  <h3>Historial</h3>

  <ul>
    <li v-for="(item, index) in historial" :key="index">
      {{ item }}
    </li>
  </ul>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
